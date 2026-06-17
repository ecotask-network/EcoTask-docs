# Stellar & Soroban Basics

## What is Stellar?
Stellar is a decentralized, open-source blockchain network designed for fast, low-cost cross-border payments and asset tokenization. Soroban is Stellar's smart contract platform.

## Key Concepts

### Accounts
Each Stellar account has a public key (G...) and a secret key (S...). Accounts require a minimum balance of 1 XLM.

### Operations
Transactions contain one or more operations: payments, asset transfers, smart contract invocations, etc.

### Soroban Contracts
Smart contracts on Stellar are written in Rust and compiled to WASM. Contracts are invoked via the Stellar network.

## Setting Up a Testnet Account
```bash
# Install Soroban CLI
cargo install --locked soroban-cli

# Generate a test identity
soroban config identity generate alice

# Fund with Friendbot
curl "https://friendbot-future.stellar.org?addr=$(soroban config identity address alice)"
```

## EcoTask Contract Architecture
Three contracts work together:
1. **eco-token** — The ECO reward token
2. **task-registry** — On-chain task database and completion tracking
3. **reward-engine** — Proof verification and automated payouts
