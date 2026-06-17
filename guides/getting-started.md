# Getting Started with EcoTask

This guide walks you through setting up the entire EcoTask stack locally.

## Prerequisites
- Node.js 20+, Rust 1.75+, React Native CLI
- PostgreSQL 15, Redis 7
- Stellar testnet account

## Step 1: Smart Contracts
1. `cd EcoTask-contract`
2. `cargo build --target wasm32-unknown-unknown --release`
3. `cargo test`
4. Deploy to testnet (see [contracts-setup.md](./contracts-setup.md))

## Step 2: Backend
1. `cd EcoTask-backend`
2. `cp .env.example .env` and fill in values
3. `docker-compose up -d` (Postgres + Redis)
4. `npm install && npx prisma migrate dev && npm run dev`

## Step 3: Mobile App
1. `cd EcoTask-app`
2. `cp .env.example .env`
3. `npm install`
4. `npm start`
5. `npm run android` (or `npm run ios`)

## Step 4: Verify
- Backend health: `curl http://localhost:3000/`
- API docs: `http://localhost:3000/api/docs`
- App connects and shows tasks
