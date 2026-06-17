# API Overview

## Base URL
```
http://localhost:3000
```

## Authentication
All protected endpoints require a JWT obtained by signing a challenge with your Stellar wallet private key.

### Flow
1. `GET /auth/challenge?wallet=GXYZ...` — Get a challenge string
2. Sign the challenge with your Stellar keypair
3. `POST /auth/login` with `{ wallet, signature, challenge }` — Receive JWT
4. Include `Authorization: Bearer <token>` in protected requests

## Rate Limiting
- General API: 100 requests per 15 minutes
- Auth endpoints: 10 requests per 15 minutes
- Proof submission: 50 requests per hour

## Error Responses
All errors follow a standard format:
```json
{ "error": "message", "details": [] }
```

### Status Codes
| Code | Meaning |
|------|---------|
| 400 | Validation error |
| 401 | Invalid or expired token |
| 404 | Resource not found |
| 409 | Resource already exists |
| 413 | File too large |
| 429 | Rate limit exceeded |
| 500 | Internal server error |
