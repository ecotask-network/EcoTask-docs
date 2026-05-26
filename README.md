<div align="center">

# 📄 ecotask-docs

**The official documentation hub for the EcoTask Network.**

*Architecture guides, API references, whitepaper, onboarding tutorials, and everything you need to understand, contribute to, or build on EcoTask.*

[![Docs Status](https://img.shields.io/badge/Docs-In%20Progress-yellow)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Built on Stellar](https://img.shields.io/badge/Built%20on-Stellar-7B68EE?logo=stellar)](https://stellar.org)

</div>

---

## 🌍 Overview

`ecotask-docs` is the single source of truth for all EcoTask documentation. Whether you're a developer integrating with our API, a contributor writing smart contracts, a community organizer onboarding local users, or a researcher studying the platform — this is where you start.

---

## 📚 What's Inside

```
ecotask-docs/
├── whitepaper/
│   └── ecotask-whitepaper.md         # Full project whitepaper
│
├── architecture/
│   ├── system-overview.md            # High-level system architecture
│   ├── smart-contracts.md            # Soroban contract design & flows
│   ├── verification-system.md        # How proof verification works
│   └── token-economy.md              # ECO token model & economics
│
├── api/
│   ├── overview.md                   # API conventions & authentication
│   ├── tasks.md                      # Tasks endpoint reference
│   ├── proofs.md                     # Proofs endpoint reference
│   ├── users.md                      # Users endpoint reference
│   └── analytics.md                  # Analytics endpoint reference
│
└── guides/
    ├── getting-started.md            # Quick start for new contributors
    ├── mobile-app-setup.md           # Setting up ecotask-app locally
    ├── contracts-setup.md            # Setting up ecotask-contracts locally
    ├── backend-setup.md              # Setting up ecotask-backend locally
    ├── stellar-basics.md             # Stellar & Soroban primer for beginners
    ├── task-creation-guide.md        # How to create & publish tasks (NGOs/sponsors)
    └── community-validator-guide.md  # How to become a community validator
```

---

## 🗺️ Documentation Map

### 📘 Whitepaper
The EcoTask whitepaper covers the full vision, problem statement, solution design, token economics, governance model, and long-term roadmap. Start here if you're new to the project or evaluating it for a partnership.

→ [Read the Whitepaper](./whitepaper/ecotask-whitepaper.md)

---

### 🏗️ Architecture

#### System Overview
A bird's-eye view of how all EcoTask components interact — from the mobile app to the Stellar blockchain.

```
┌──────────────────────────────────────────────────────────────────┐
│                        EcoTask System                            │
│                                                                  │
│  ┌─────────────┐     ┌─────────────────┐     ┌───────────────┐  │
│  │  Mobile App │────▶│    Backend API  │────▶│    Stellar    │  │
│  │ (React      │     │   (Node.js)     │     │  Blockchain   │  │
│  │  Native)    │◀────│                 │◀────│  (Soroban)    │  │
│  └─────────────┘     └────────┬────────┘     └───────────────┘  │
│                               │                                  │
│                      ┌────────┼────────┐                        │
│                      ▼        ▼        ▼                        │
│                  ┌──────┐ ┌──────┐ ┌──────┐                    │
│                  │  DB  │ │Redis │ │ IPFS │                    │
│                  │(PG)  │ │Queue │ │Proof │                    │
│                  └──────┘ └──────┘ └──────┘                    │
└──────────────────────────────────────────────────────────────────┘
```

→ [Full Architecture Guide](./architecture/system-overview.md)

#### Smart Contracts
How the three Soroban contracts (`eco-token`, `task-registry`, `reward-engine`) interact, their interfaces, and security considerations.

→ [Smart Contract Design](./architecture/smart-contracts.md)

#### Verification System
How EcoTask ensures that claimed tasks were actually completed — from photo analysis and GPS validation to community validators and on-chain proof hashes.

→ [Verification System Docs](./architecture/verification-system.md)

#### Token Economy
How ECO tokens are minted, distributed, and governed. Includes supply model, reward curve, governance rights, and carbon credit integration plans.

→ [Token Economy Docs](./architecture/token-economy.md)

---

### 📡 API Reference

All EcoTask API endpoints documented with request/response examples.

| Endpoint Group | Description |
|---------------|-------------|
| [Tasks API](./api/tasks.md) | Browse, create, and manage climate-action tasks |
| [Proofs API](./api/proofs.md) | Submit and track proof of task completion |
| [Users API](./api/users.md) | Profiles, wallet linking, and impact history |
| [Analytics API](./api/analytics.md) | Platform-wide and per-user impact statistics |

**Authentication**

All protected endpoints require a JWT obtained by signing a challenge with your Stellar wallet private key:

```bash
# Step 1: Get a challenge
GET /api/auth/challenge?wallet=GXYZ...

# Step 2: Sign the challenge with your Stellar keypair and submit
POST /api/auth/login
{
  "wallet": "GXYZ...",
  "signature": "...",
  "challenge": "..."
}

# Returns: { "token": "eyJ..." }
```

→ [Full Auth Guide](./api/overview.md)

---

### 🧭 Guides

| Guide | Audience |
|-------|---------|
| [Getting Started](./guides/getting-started.md) | All contributors — start here |
| [Mobile App Setup](./guides/mobile-app-setup.md) | Frontend / React Native developers |
| [Contracts Setup](./guides/contracts-setup.md) | Blockchain / Rust developers |
| [Backend Setup](./guides/backend-setup.md) | Backend / Node.js developers |
| [Stellar Basics](./guides/stellar-basics.md) | Developers new to Stellar & Soroban |
| [Task Creation Guide](./guides/task-creation-guide.md) | NGOs, sponsors, and task curators |
| [Community Validator Guide](./guides/community-validator-guide.md) | Community members who verify tasks |

---

## 🌱 EcoTask Ecosystem

| Repo | Description |
|------|-------------|
| [`ecotask-app`](https://github.com/ecotask-network/ecotask-app) | 📱 React Native mobile dApp |
| [`ecotask-contracts`](https://github.com/ecotask-network/ecotask-contracts) | 🔗 Stellar Soroban smart contracts |
| [`ecotask-backend`](https://github.com/ecotask-network/ecotask-backend) | ⚙️ Node.js API & verification engine |
| [`ecotask-docs`](https://github.com/ecotask-network/ecotask-docs) | 📄 You are here |

---

## ✍️ Contributing to Docs

Good documentation is as important as good code. We welcome:

- 🐛 Fixing typos, broken links, or outdated information
- 📖 Expanding thin sections or adding missing guides
- 🌐 Translating docs into Swahili, French, Portuguese, or Hindi
- 🎨 Improving diagrams and architecture visuals

### How to Contribute

```bash
# 1. Fork and clone
git clone https://github.com/ecotask-network/ecotask-docs.git
cd ecotask-docs

# 2. Create a branch
git checkout -b docs/improve-verification-guide

# 3. Make your changes (Markdown files)

# 4. Submit a pull request
```

All documentation is written in **Markdown**. Keep language clear, concise, and accessible — many of our users and contributors are not native English speakers.

---

## 📄 License

MIT — see [LICENSE](./LICENSE) for details.

---

<div align="center">

*Part of the [EcoTask Network](https://github.com/ecotask-network) — Because the environment deserves an economy.*

</div>
