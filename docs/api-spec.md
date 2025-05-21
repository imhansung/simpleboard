# 📘 게시판 프로젝트 API 명세서

- **Base URL**: `/api`
- **Content-Type**: `application/json`
- **인증 방식**: JWT 토큰 (헤더: `Authorization: Bearer <token>`)

---

## ✅ 인증 API

### 🔐 회원가입

- `POST /auth/register`

```json
요청 Body:
{
  "username": "string",
  "password": "string",
  "email": "user@example.com"
}
응답:
{
  "id": 1,
  "username": "string",
  "email": "user@example.com"
}
```

### 🔐 로그인
- `POST /auth/login`

```json
요청 Body:
{
  "username": "string",
  "password": "string"
}

응답:
{
  "accessToken": "JWT_TOKEN",
  "expiresIn": 3600
}
```

## 📄 게시글 API
###  📄 게시글 목록 조회
- `GET /posts?page=0&size=10`

#### ✅ 인증 필요 없음
```json
응답:
[
  {
    "id": 1,
    "title": "첫 글입니다",
    "author": "user1",
    "createdAt": "2025-05-21T10:00:00"
  },
  ...
]

```

### 📄 게시글 상세 조회
- `GET /posts/{id}`
```json
응답:
{
  "id": 1,
  "title": "첫 글입니다",
  "content": "내용입니다",
  "author": "user1",
  "createdAt": "2025-05-21T10:00:00",
  "comments": [ ... ]
}
```

### ✏️ 게시글 작성
- `POST /posts`
- `✅ 인증 필요`
```json
요청 Body:
{
  "title": "제목입니다",
  "content": "내용입니다"
}
응답:
{
  "id": 2,
  "message": "게시글이 등록되었습니다."
}

```

### 🛠️ 게시글 수정
- `PUT /posts/{id}`
- `✅ 인증 필요 (본인 게시글만 가능)`

```json
요청 Body:
{
  "title": "수정된 제목",
  "content": "수정된 내용"
}

```

### ❌ 게시글 삭제
- `DELETE /posts/{id}`
- `✅ 인증 필요 (본인 또는 관리자)`

### 💬 댓글 API
#### 💬 댓글 작성
- `POST /posts/{postId}/comments`
- `✅ 인증 필요`

```json
요청 Body:
{
  "content": "댓글 내용입니다."
}

```

### ❌ 댓글 삭제
- `DELETE /comments/{id}`
- `✅ 인증 필요 (본인 또는 관리자)`

### 🧑 사용자 API
#### 👤 사용자 프로필 조회
- `GET /users/me`
- `✅ 인증 필요`
```json
응답:
{
  "id": 1,
  "username": "user1",
  "email": "user@example.com"
}
```

### 🔒 오류 코드 예시
| 코드  | 메시지                   | 설명        |
| --- | --------------------- | --------- |
| 400 | Validation failed     | 입력값 오류    |
| 401 | Unauthorized          | JWT 누락/만료 |
| 403 | Forbidden             | 권한 없음     |
| 404 | Not Found             | 리소스 없음    |
| 500 | Internal Server Error | 서버 오류     |


### ⚙️ 추후 확장 예정 기능: 좋아요(Like), 태그 검색, 파일 업로드, 알림 기능 등

