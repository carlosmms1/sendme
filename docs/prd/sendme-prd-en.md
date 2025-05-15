# 📝 PRD — Sendme (URL Shortener)

## 📌 Overview

Create a backend service that allows long URLs to be shortened into short, unique codes. The system must be simple, performant, have a clear separation of concerns, well-written documentation, and be ready to evolve in stages.

The MVP will be developed with a focus on productivity using **Go**, **Echo**, **GORM**, **Redis** and **Swagger**.

## 🎯 Goal

- Convert long URLs into short, unique codes.
- Automatically redirect to the original URL when accessing the shortened URL.
- Support caching for performance.
- Allow optional URL expiration configuration.
- Ensure a scalable and extensible architecture.

## 🏗️ Tech Stack

| Layer                | Technology                                        |
| -------------------- | ------------------------------------------------- |
| **Language**         | Go (Golang)                                       |
| **Web Framework**    | [Echo](https://echo.labstack.com/)                |
| **ORM**              | [GORM](https://gorm.io/)                          |
| **Database**         | PostgreSQL                                        |
| **Caching**          | Redis                                             |
| **Documentation**    | Swagger (`swaggo/echo-swagger`)                   |
| **Testing**          | Go test                                           |
| **Containerization** | Docker + Docker Compose                           |
| **Environment**      | `.env` with support for variables like `BASE_URL` |

## 📁 Project Structure

```
sendme/
├── cmd/
│   └── main.go                   # Application entry point
├── internal/
│   ├── handler/                  # Echo handlers (controllers)
│   ├── service/                  # Business logic
│   ├── repository/               # GORM + Redis (interfaces + implementations)
│   ├── model/                    # Entity structs
│   ├── cache/                    # Redis integration
│   └── config/                   # Environment, DB, and Redis setup
├── docs/                         # Swagger (auto-generated)
├── test/                         # Unit tests
├── go.mod / go.sum
├── .env
├── Dockerfile
└── docker-compose.yml
```

## 🔄 Feature Flow

### 1. **Shorten a URL**

- **Endpoint**: `POST /api/shorten`
- **Payload**:

```json
{
  "original_url": "https://example.com/article/123",
  "ttl": 3600
}
```

- **Response**:

```json
{
  "short_url": "https://sh.rt/abc123",
  "expires_at": "2025-05-14T13:00:00Z"
}
```

### 2. **Redirect**

- **Endpoint**: `GET /:code`
- **Behavior**:
  - Check Redis → if found, redirect.
  - Otherwise, check the database → if found, store in Redis and redirect.
  - Otherwise, return 404.

## ⚙️ Environment Variables (.env)

```env
BASE_URL=https://send.me/
DATABASE_URL=postgres://user:password@db:5432/url_db
REDIS_URL=redis://redis:6379
PORT=8080
```

## ✅ Confirmed Features for the MVP

| Requirement               | Status       |
| ------------------------- | ------------ |
| Shorten URL               | ✅ Confirmed |
| Optional TTL via payload  | ✅ Confirmed |
| Redirect via short code   | ✅ Confirmed |
| Caching with Redis        | ✅ Confirmed |
| Storage in PostgreSQL     | ✅ Confirmed |
| Use of GORM               | ✅ Confirmed |
| Swagger for documentation | ✅ Confirmed |
| Tests with `go test`      | ✅ Confirmed |
| Environment variables     | ✅ Confirmed |
| Docker + docker-compose   | ✅ Confirmed |

## 📈 Possible Future Extensions (Not in MVP)

- Support for analytics (track how many times each link was accessed)
- Password-protected or authenticated URLs
- Temporary self-destructing links
- Web dashboard for managing URLs
- Public statistics accessible via QR code
