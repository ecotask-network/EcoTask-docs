# Users API

## GET /users/:id
Get user profile.

### Response
```json
{
  "id": "uuid",
  "name": "string",
  "wallet": "GABCD...",
  "bio": "string",
  "avatarUrl": "string",
  "stats": {
    "tasksCompleted": 12,
    "treesPlanted": 5,
    "plasticCollected": 20,
    "co2Reduced": 50
  },
  "createdAt": "2026-06-17T00:00:00Z"
}
```

## PUT /users/:id
Update user profile.

### Headers
`Authorization: Bearer <token>`

### Body
```json
{
  "name": "string",
  "bio": "string",
  "avatarUrl": "string"
}
```

## GET /users/:id/impact
Get user's environmental impact summary.

### Response
```json
{
  "totalRewards": 500,
  "treesPlanted": 5,
  "plasticCollected": 20,
  "co2Reduced": 50,
  "rank": 42
}
```
