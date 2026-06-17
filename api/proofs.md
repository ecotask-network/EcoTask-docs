# Proofs API

## POST /proofs
Submit proof of task completion.

### Headers
`Authorization: Bearer <token>`  
`Content-Type: multipart/form-data`

### Body
| Field | Type | Description |
|-------|------|-------------|
| photos | file[] | Up to 5 JPEG/PNG/WebP images (max 10MB each) |
| taskId | string | UUID of the task |
| lat | number | GPS latitude (optional) |
| lng | number | GPS longitude (optional) |
| notes | string | Additional notes (optional) |

### Response
```json
{
  "id": "uuid",
  "status": "pending",
  "taskId": "uuid",
  "photos": ["cid1", "cid2"],
  "createdAt": "2026-06-17T00:00:00Z"
}
```

## GET /proofs/:id
Get proof status and details.

### Response
```json
{
  "id": "uuid",
  "status": "approved",
  "taskId": "uuid",
  "photos": ["cid1"],
  "rewardAmount": 50,
  "createdAt": "2026-06-17T00:00:00Z",
  "resolvedAt": "2026-06-17T01:00:00Z"
}
```

## GET /proofs/user/:userId
Get all proofs for a user.
