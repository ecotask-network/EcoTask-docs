# EcoTask Whitepaper

## Climate Action, Verified. Rewarded. On-Chain.

**Version 1.0 — June 2026**

---

## Abstract

EcoTask is a decentralized platform that connects communities in developing regions with climate-action tasks — planting trees, cleaning plastic, restoring ecosystems — and rewards them instantly via Stellar blockchain payments. By combining a mobile-first experience, photo-based proof verification, and transparent on-chain payouts, EcoTask removes the trust barrier that prevents climate funding from reaching local communities.

---

## 1. Problem

### 1.1 The Climate Funding Gap

Billions of dollars flow annually from developed nations to climate mitigation projects in the Global South. Yet, a tiny fraction reaches the individuals doing the work:

- **Intermediary overhead**: NGOs, carbon credit brokers, and verification agencies take 40–60% of funds before they reach the field.
- **Payment delays**: Field workers often wait weeks or months for payment, creating cash-flow problems that make climate work unsustainable.
- **Trust deficit**: Donors have no visibility into whether their money resulted in real climate impact. Fraud and double-counting erode confidence.

### 1.2 The Unbanked Climate Worker

An estimated 1.4 billion adults remain unbanked globally. Many live in climate-vulnerable regions and are actively engaged in restoration work — but lack the financial infrastructure to receive digital payments. Stellar's low-fee, lightweight blockchain provides an on-ramp for anyone with a smartphone.

### 1.3 Verification Without Middlemen

Current verification models rely on centralized auditors or satellite imagery — both expensive and slow. EcoTask proposes a hybrid model: automated GPS + photo verification, augmented by community validators, with all proof hashes stored immutably on-chain.

---

## 2. Solution

### 2.1 System Overview

EcoTask consists of four integrated components:

1. **Mobile App** (React Native) — Task discovery, photo capture, GPS tagging, wallet management
2. **Backend API** (Node.js/Express) — Task management, proof intake, verification queue, Stellar oracle
3. **Smart Contracts** (Soroban/Rust) — ECO token, task registry, reward engine
4. **Documentation Hub** — Whitepaper, API references, setup guides

### 2.2 User Flow

1. A user browses available climate-action tasks on the mobile app (e.g., "Plant 10 Mangrove Trees in Mombasa")
2. They go to the task location, perform the work, and capture photo evidence with GPS metadata
3. The proof is submitted to the backend, pinned to IPFS, and queued for verification
4. Auto-verification checks GPS coordinates and photo validity; inconclusive proofs route to community validators
5. Once approved, the backend oracle calls the Soroban reward-engine contract
6. The contract mints ECO tokens (or transfers USDC) directly to the user's Stellar wallet
7. The user sees their balance update in real-time and can track their lifetime impact

### 2.3 Key Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Blockchain | Stellar (Soroban) | Low fees (~$0.00001), fast finality (3–5s), mobile-friendly |
| Token Standard | SEP-41 (Stellar Token) | Interoperable with Stellar ecosystem wallets and DEX |
| Proof Storage | IPFS (via Web3.Storage) | Decentralized, content-addressed, permanent |
| Mobile Framework | React Native | Cross-platform from single codebase, large community |
| Verification | Hybrid (auto + community) | Speed of automation + judgment of human review |

---

## 3. Token Model

### 3.1 ECO Token

- **Name**: EcoTask Token
- **Symbol**: ECO
- **Decimals**: 7
- **Standard**: SEP-41 (Stellar Token Interface)
- **Fixed Supply Cap**: 100,000,000 ECO

### 3.2 Minting Mechanism

ECO tokens are minted exclusively by the reward-engine smart contract when a proof is verified. No pre-mine. No admin minting. The minting rate follows a reward curve:

```
reward = base_rate * difficulty_multiplier * impact_multiplier
```

- `base_rate`: 10 ECO per standard task
- `difficulty_multiplier`: 1.0–3.0 based on task complexity
- `impact_multiplier`: 1.0–5.0 based on environmental impact

### 3.3 Token Distribution

| Allocation | Percentage | Vesting |
|------------|-----------|---------|
| Task Rewards | 60% | Minted over time as tasks verified |
| Team & Contributors | 20% | 2-year linear vesting, 6-month cliff |
| Ecosystem Fund | 10% | DAO-governed (future) |
| Initial Liquidity | 10% | Unlocked at TGE |

### 3.4 Reward Curve

To incentivize early adoption while ensuring long-term sustainability, the minting rate decreases as total supply increases:

```
mintable_supply = max_supply - current_supply
effective_rate = base_rate * (mintable_supply / max_supply)
```

This ensures the last tokens are minted only at very high adoption, creating a natural S-curve of rewards.

---

## 4. Verification System

### 4.1 Automated Checks

1. **GPS Validation**: Submitted coordinates must fall within the task's defined radius (typically ±100m)
2. **Photo Quality**: Image must be non-blurry, contain valid EXIF metadata
3. **Proof Uniqueness**: Photo hash must not match any previously submitted proof
4. **Timeliness**: Proof must be submitted before task expiry

### 4.2 Community Validators

When automated checks are inconclusive, the proof enters a community validator queue. Validators are trusted community members who review photos and make a pass/fail judgment. They earn a small validator fee for each review.

### 4.3 On-Chain Proof Storage

The IPFS CID of each proof photo is stored on-chain in the reward-engine contract at submission time. This creates an immutable audit trail that prevents retroactive fraud — if a proof hash changes, it won't match the on-chain record.

---

## 5. Smart Contract Architecture

### 5.1 ECO Token (`eco-token`)

Standard Stellar token with restricted minting:
- `initialize(admin, name, symbol, decimal)` — one-time setup
- `mint(to, amount)` — only reward-engine contract can call
- `transfer(from, to, amount)` — standard transfer with authorization
- `balance(id)` — query token balance

### 5.2 Task Registry (`task-registry`)

On-chain task database with access control:
- `create_task(creator, type, location_hash, reward, max_completions, expires)` — admin/sponsor only
- `complete_task(task_id, user)` — marks task as completed by user
- `expire_task(task_id)` — admin expiration
- Prevents double-claiming and overflow of max completions

### 5.3 Reward Engine (`reward-engine`)

Verification and payout logic:
- `submit_proof(oracle, user, task_id, proof_cid)` — oracle records proof hash
- `approve_proof(oracle, user, task_id)` — oracle confirms, triggers mint
- `reject_proof(oracle, user, task_id)` — oracle rejects
- `dispute_proof(caller, user, task_id)` — admin disputes a verification

---

## 6. Roadmap

### Phase 1: MVP (Current — Q3 2026)
- Three Soroban contracts deployed to testnet
- Backend API with task CRUD, proof submission, auto-verification
- React Native app with wallet connect, task browsing, proof capture
- End-to-end flow: browse → complete → submit → verify → get paid

### Phase 2: Community Validators (Q4 2026)
- Community validator dashboard
- Validator staking and reward mechanism
- Dispute resolution flow
- Mobile app improvements (offline queue, push notifications)

### Phase 3: DAO Governance (Q1 2027)
- ECO token holders can vote on platform parameters
- Community-governed task creation
- Ecosystem fund allocation via proposals

### Phase 4: Carbon Credit Integration (Q2 2027+)
- Verified climate actions tokenized as carbon credits
- Integration with carbon credit marketplaces
- Corporate sponsors can purchase verified offsets

---

## 7. Security

### 7.1 Smart Contract Security
- All minting restricted to reward-engine contract only
- Overflow checks on all arithmetic operations
- Role-based access control (admin, sponsor, oracle)
- Proof hashes stored at submission — immutable audit trail

### 7.2 Backend Security
- JWT-based authentication with Stellar wallet signature
- Rate limiting on auth and proof endpoints
- Input validation via Zod schemas
- Encrypted environment variables for secrets

### 7.3 User Security
- Non-custodial: users control their own private keys
- Optional in-app wallet creation for first-time users
- Push notification alerts for all wallet activity

---

## 8. Tokenomics Summary

- **Total Supply**: 100,000,000 ECO (fixed cap)
- **Initial Circulating**: ~10,000,000 ECO (liquidity + ecosystem)
- **Minting Start**: At platform launch (testnet)
- **Reward Rate**: Starts at 10 ECO/task, decreases as supply grows
- **Validator Fees**: 2% of task reward allocated to validators

---

## 9. Conclusion

EcoTask creates a trust-minimized economic layer for climate action. By combining Stellar's low-cost blockchain, mobile-first design, and a hybrid verification system, we can route climate funding directly to the communities doing the work — with transparency, speed, and minimal overhead.

The environment deserves an economy. EcoTask is that economy.

---

*Part of the [EcoTask Network](https://github.com/ecotask-network)*
