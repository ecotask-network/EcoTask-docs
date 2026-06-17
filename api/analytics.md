# Analytics API

## GET /analytics/overview
Platform-wide impact statistics.

### Headers
`Authorization: Bearer <token>` (admin only)

### Response
```json
{
  "totalUsers": 1250,
  "totalTasks": 340,
  "totalCompletions": 2800,
  "totalRewardsPaid": 140000,
  "treesPlanted": 5200,
  "plasticCollected": 1800,
  "co2Reduced": 4500,
  "activeValidators": 85
}
```

## GET /analytics/tasks
Task completion and reward distribution data.

## GET /analytics/users
User growth and engagement metrics.
