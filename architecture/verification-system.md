# Verification System

## Flow
1. User submits proof (photo + GPS) from mobile app
2. Proof saved to DB with status `pending`
3. Photo + GPS pinned to IPFS
4. Job added to BullMQ verification queue
5. Auto-checks run (GPS in task zone ±100m, photo contains vegetation/trash via stub)
6. If auto-check passes → approved; if inconclusive → queued for community validator
7. Approved → rewardWorker triggers Stellar oracle call
8. ECO tokens minted and sent to user's wallet
9. User notified via push notification

## Validator Roles
- **Auto-validator**: automated GPS + basic image checks
- **Community validators**: humans reviewing flagged proofs via a dashboard
