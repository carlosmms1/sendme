# 📝 PRD — Encurtador de URLs (URL Shortener)

## 📌 Visão Geral

Criar um serviço backend que permita encurtar URLs longas em códigos curtos e únicos. O sistema deve ser simples, performático, com boa separação de responsabilidades, documentação clara e pronto para ser evoluído em etapas.

O MVP será desenvolvido com foco em produtividade usando **Go**, **Echo**, **GORM**, **Redis** e **Swagger**.

## 🎯 Objetivo

- Transformar URLs longas em códigos curtos e únicos.
- Redirecionar automaticamente para a URL original ao acessar a URL curta.
- Suportar cache para performance.
- Permitir configuração opcional de expiração da URL.
- Garantir estrutura escalável e extensível.

## 🏗️ Stack Tecnológica

| Camada              | Tecnologia                                     |
| ------------------- | ---------------------------------------------- |
| **Linguagem**       | Go (Golang)                                    |
| **Framework Web**   | [Echo](https://echo.labstack.com/)             |
| **ORM**             | [GORM](https://gorm.io/)                       |
| **Banco de dados**  | PostgreSQL                                     |
| **Cache**           | Redis                                          |
| **Documentação**    | Swagger (`swaggo/echo-swagger`)                |
| **Testes**          | Go test                                        |
| **Containerização** | Docker + Docker Compose                        |
| **Ambiente**        | `.env` com suporte a variáveis como `BASE_URL` |

## 📁 Estrutura do Projeto

```
url-shortener/
├── cmd/
│   └── main.go                   # Inicialização da aplicação
├── internal/
│   ├── handler/                  # Echo handlers (controllers)
│   ├── service/                  # Lógica de negócio
│   ├── repository/               # GORM + Redis (interface + implementação)
│   ├── model/                    # Structs das entidades
│   ├── cache/                    # Integração com Redis
│   └── config/                   # Setup de env, DB e Redis
├── docs/                         # Swagger (auto-gerado)
├── test/                         # Testes unitários
├── go.mod / go.sum
├── .env
├── Dockerfile
└── docker-compose.yml
```

## 🔄 Fluxo de Funcionalidades

### 1. **Encurtar uma URL**

- **Endpoint**: `POST /api/shorten`
- **Payload**:

```json
{
  "original_url": "https://exemplo.com/artigo/123",
  "ttl": 3600 // (opcional, em segundos)
}
```

- **Resposta**:

```json
{
  "short_url": "https://sh.rt/abc123",
  "expires_at": "2025-05-14T13:00:00Z" // se TTL fornecido
}
```

### 2. **Redirecionar**

- **Endpoint**: `GET /:code`
- **Comportamento**:
  - Verifica Redis → se encontrar, redireciona.
  - Senão, consulta DB → se encontrar, salva no Redis e redireciona.
  - Senão, retorna 404.

## ⚙️ Variáveis de Ambiente (.env)

```env
BASE_URL=https://sh.rt/
DATABASE_URL=postgres://user:password@db:5432/url_db
REDIS_URL=redis://redis:6379
PORT=8080
```

## ✅ Funcionalidades Confirmadas para o MVP

| Requisito                       | Status        |
| ------------------------------- | ------------- |
| Encurtar URL                    | ✅ Confirmado |
| TTL opcional por payload        | ✅ Confirmado |
| Redirecionamento via short code | ✅ Confirmado |
| Cache com Redis                 | ✅ Confirmado |
| Armazenamento em PostgreSQL     | ✅ Confirmado |
| Uso de GORM                     | ✅ Confirmado |
| Swagger para documentação       | ✅ Confirmado |
| Testes com `go test`            | ✅ Confirmado |
| Variáveis de ambiente           | ✅ Confirmado |
| Docker + docker-compose         | ✅ Confirmado |

## 📈 Futuras extensões possíveis (não MVP)

- Suporte a analytics (quantas vezes cada link foi acessado)
- URLs com senha ou autenticação
- Links temporários auto-destrutivos
- Painel web de gerenciamento de URLs
- Estatísticas públicas via QR code
