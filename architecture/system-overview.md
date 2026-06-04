# EcoTask System Architecture

## High-Level Overview

```
                        ┌──────────────────────────────────────────────────┐
                        │                       EcoTask                     │
                        │                                                  │
                        │  ┌─────────────┐       ┌─────────────────┐      │
                        │  │  Mobile App  │──────▶│  Backend API    │      │
                        │  │  (React      │       │  (Node.js)      │      │
                        │  │   Native)    │◀──────│                 │      │
                        │  └─────────────┘       └────────┬────────┘      │
                        │                                  │               │
                        │                         ┌────────┼────────┐      │
                        │                         ▼        ▼        ▼      │
                        │                   ┌──────┐ ┌──────┐ ┌──────┐    │
                        │                   │  DB  │ │Redis │ │ IPFS │    │
                        │                   │ (PG) │ │Queue │ │Proof │    │
                        │                   └──────┘ └──────┘ └──────┘    │
                        │                                  │               │
                        │                                  ▼               │
                        │                         ┌─────────────────┐      │
                        │                         │  Stellar        │      │
                        │                         │  Blockchain     │      │
                        │                         │  (Soroban)      │      │
                        │                         └─────────────────┘      │
                        │                              │                   │
                        │                     ┌────────┼────────┐          │
                        │                     ▼        ▼        ▼          │
                        │               ┌────────┐ ┌────────┐ ┌────────┐  │
                        │               │  ECO   │ │  Task  │ │ Reward │  │
                        │               │ Token  │ │Registry│ │ Engine │  │
                        │               └────────┘ └────────┘ └────────┘  │
                        └──────────────────────────────────────────────────┘
```

## Component Breakdown

### 1. Mobile App (`EcoTask-app`)

- **Framework**: React Native 0.73 (cross-platform iOS + Android)
- **Navigation**: React Navigation v6 with bottom-tab and stack navigators
- **State**: Zustand with MMKV persistent storage
- **Camera**: Vision Camera for photo capture with EXIF GPS metadata
- **Wallet**: Freighter browser extension, Lobstr, or in-app wallet creation

**Screens**:
- `OnboardingScreen` — Wallet connection gateway
- `HomeScreen` — Impact dashboard (trees planted, plastic collected, CO₂ offset)
- `TaskListScreen` — Filterable, paginated task feed
- `TaskDetailScreen` — Task instructions and "Start Task" CTA
- `SubmitProofScreen` — Camera + GPS capture with submission progress
- `WalletScreen` — Balance display, transaction history

### 2. Backend API (`EcoTask-backend`)

- **Runtime**: Node.js 20 with Express 4
- **Database**: PostgreSQL 15 via Prisma ORM
- **Queue**: BullMQ (backed by Redis 7) for async proof verification
- **File Storage**: IPFS via Web3.Storage for permanent proof storage
- **Auth**: JWT with Stellar wallet signature verification

**API Endpoints**:
| Route | Method | Description |
|-------|--------|-------------|
| `GET /` | Health | Service health check |
| `GET /auth/challenge` | Auth | Get signing challenge |
| `POST /auth/login` | Auth | Authenticate with Stellar signature |
| `GET/POST /tasks` | Tasks | List and create tasks |
| `GET/PUT/DELETE /tasks/:id` | Tasks | Single task operations |
| `POST /proofs` | Proofs | Submit proof with photo |
| `GET /proofs/:id` | Proofs | Get proof status |
| `GET /users/:id` | Users | Get user profile |
| `GET /users/:id/impact` | Users | Get user impact stats |

### 3. Smart Contracts (`EcoTask-contract`)

- **Language**: Rust
- **Platform**: Stellar Soroban
- **Build Target**: WebAssembly (wasm32-unknown-unknown)

**Contracts**:

**ECO Token** — Standard SEP-41 token with restricted minting:
- Only the reward-engine contract can mint new tokens
- Standard transfer and balance operations
- Immutable metadata (name, symbol, decimals)

**Task Registry** — On-chain task database:
- Stores task definitions with reward parameters
- Role-based access control (admin, sponsor)
- Prevents double-claiming and overflow of completions
- Emits events for task lifecycle changes

**Reward Engine** — Verification and payout engine:
- Receives verification results from the off-chain oracle
- Validates proof hashes against IPFS CIDs
- Mints ECO tokens on successful verification
- Handles disputes and partial rewards

### 4. Documentation Hub (`EcoTask-docs`)

- Whitepaper with token model and roadmap
- Architecture documentation
- API reference with request/response examples
- Setup guides for all components

---

## Data Flow: Full User Journey

```
1. User opens app → OnboardingScreen
2. User connects Freighter wallet → Stellar public key stored in Zustand
3. TaskListScreen fetches tasks from GET /api/tasks
4. User taps a task → navigates to TaskDetailScreen
5. User taps "Start Task" → navigates to SubmitProofScreen
6. User takes photo with camera → GPS metadata extracted
7. User taps "Submit" → FormData with photo + GPS sent to POST /api/proofs
8. Backend saves Proof to DB (status: PENDING), pins photo to IPFS
9. Backend enqueues verification job in BullMQ
10. verificationWorker runs auto-checks (GPS zone, photo quality)
11. If approved: status → APPROVED, rewardWorker enqueued
12. rewardWorker calls Stellar oracle → reward-engine.approve_proof()
13. Reward engine mints ECO tokens to user's Stellar wallet
14. App refreshes balance → user sees reward confirmed
```

---

## Tech Stack Summary

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Mobile App | React Native 0.73 | Cross-platform UI |
| State | Zustand + MMKV | Global state + persistence |
| Navigation | React Navigation 6 | Screen routing |
| Camera | Vision Camera 3 | Photo proof capture |
| Backend | Node.js 20 + Express 4 | REST API |
| Database | PostgreSQL 15 + Prisma | Relational data |
| Queue | BullMQ + Redis 7 | Async job processing |
| File Storage | IPFS (Web3.Storage) | Decentralized proof storage |
| Blockchain | Stellar Soroban | Smart contracts |
| Smart Contracts | Rust + Soroban SDK | Token, registry, rewards |
| Wallet | Freighter / Lobstr / In-app | Stellar wallet |
| Auth | JWT + Stellar signatures | User authentication |
| Testing | Jest + Supertest | Unit & integration tests |
| CI/CD | GitHub Actions | Automated builds & tests |
