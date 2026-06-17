# Task Creation Guide

This guide is for NGOs, sponsors, and community organizers who want to create climate-action tasks on EcoTask.

## Prerequisites
- A Stellar wallet with some XLM for transaction fees
- Admin or sponsor access to the EcoTask platform

## Creating a Task

### Via API (Admin)
```bash
curl -X POST http://localhost:3000/tasks \
  -H "Authorization: Bearer <admin-jwt>" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Plant 10 Trees in Karura Forest",
    "description": "Help reforest Karura Forest by planting 10 indigenous tree seedlings.",
    "type": "TREE_PLANTING",
    "rewardAmount": 50,
    "lat": -1.2340,
    "lng": 36.8320,
    "radiusMeters": 500,
    "maxCompletions": 20
  }'
```

## Task Types
| Type | Icon | Example |
|------|------|---------|
| TREE_PLANTING | 🌳 | Plant trees in designated areas |
| TRASH_COLLECTION | ♻️ | Collect and sort recyclable waste |
| OCEAN_CLEANUP | 🌊 | Remove trash from beaches and oceans |
| GARDENING | 🌱 | Maintain community gardens |
| EDUCATION | 📚 | Teach environmental awareness |
| OTHER | 📍 | Other climate-positive actions |

## Best Practices
- Set realistic reward amounts based on task difficulty
- Include clear instructions and location details
- Set appropriate expiration dates
- Verify task locations are accessible to the community
