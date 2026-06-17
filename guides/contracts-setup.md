# Contracts Setup Guide

## Prerequisites
- Rust 1.75+
- Soroban CLI (`cargo install --locked soroban-cli`)
- wasm32-unknown-unknown target (`rustup target add wasm32-unknown-unknown`)

## Build
```bash
cd EcoTask-contract
cargo build --target wasm32-unknown-unknown --release
```

## Test
```bash
cargo test
```

## Deploy to Testnet
```bash
# Fund your deployer account
./scripts/fund-accounts.sh GDEPLOYER...

# Deploy all three contracts
./scripts/deploy.sh eco-token testnet
./scripts/deploy.sh task-registry testnet
./scripts/deploy.sh reward-engine testnet

# Verify deployment
./scripts/verify-deploy.sh
```

## Initialize Contracts
After deployment, initialize each contract with the appropriate addresses.

## Contract Addresses
Record the deployed contract IDs — you'll need them for the backend configuration.
