# Backend Setup Guide

## Prerequisites
- Node.js 20+
- PostgreSQL 15+
- Redis 7+

## Quick Start with Docker
```bash
cd EcoTask-backend
cp .env.example .env
docker-compose up -d
npm install
npx prisma migrate dev
npm run dev
```

## Manual Setup
1. Install PostgreSQL 15+ and Redis 7+
2. Create a database: `createdb ecotask`
3. Copy `.env.example` to `.env` and update credentials
4. Run `npm install`
5. Run `npx prisma migrate dev`
6. Run `npm run db:seed` (optional, adds sample data)
7. Run `npm run dev`

## Verification
```bash
curl http://localhost:3000/
# {"status":"ok","service":"ecotask-backend"}
```

## Testing
```bash
npm test              # Unit tests
npm run test:integration  # Integration tests
npm run test:e2e          # End-to-end tests
```
