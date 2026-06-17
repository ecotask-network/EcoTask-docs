# Tasks API

## GET /tasks
List tasks with optional filters.

### Query Parameters
| Param | Type | Description |
|-------|------|-------------|
| type | string | `TREE_PLANTING`, `TRASH_COLLECTION`, `OCEAN_CLEANUP`, `GARDENING`, `EDUCATION`, `OTHER` |
| status | string | `ACTIVE`, `PAUSED`, `COMPLETED`, `EXPIRED` |
| lat, lng, radius | number | Geo-filter tasks within radius (km) |
| minReward, maxReward | number | Filter by reward range |
| search | string | Full-text search on title and description |
| page, limit | number | Pagination (default: page=1, limit=20) |

### Response
```json
{
  "tasks": [
    {
      "id": "uuid",
      "title": "Plant Trees",
      "type": "TREE_PLANTING",
      "rewardAmount": 50,
      "lat": -1.2921,
      "lng": 36.8219,
      "status": "ACTIVE",
      "distance": 2.3
    }
  ],
  "total": 42,
  "page": 1,
  "limit": 20,
  "totalPages": 3
}
```

## POST /tasks
Create a task (admin/sponsor only).

### Headers
`Authorization: Bearer <token>`

### Body
```json
{
  "title": "string",
  "description": "string",
  "type": "TREE_PLANTING",
  "rewardAmount": 50,
  "lat": -1.2921,
  "lng": 36.8219,
  "radiusMeters": 100,
  "maxCompletions": 5
}
```

## GET /tasks/:id
Get a single task by ID.

## PUT /tasks/:id
Update a task (admin/sponsor only).

## DELETE /tasks/:id
Delete a task (admin/sponsor only).
