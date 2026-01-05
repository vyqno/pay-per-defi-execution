# MNEE Pay-Per-Execution DeFi Platform

> 🚀 A pay-per-use DeFi platform gating 1inch token swaps behind MNEE payments using HTTP 402

[![Solidity](https://img.shields.io/badge/Solidity-0.8.20-blue)](https://soliditylang.org/)
[![Next.js](https://img.shields.io/badge/Next.js-15-black)](https://nextjs.org/)
[![Foundry](https://img.shields.io/badge/Foundry-latest-red)](https://book.getfoundry.sh/)
[![Status](https://img.shields.io/badge/Status-In%20Development-yellow)](https://github.com)

## 🎯 Overview

Pay 1 MNEE stablecoin to unlock 1 token swap. This platform implements HTTP 402 "Payment Required" for DeFi operations, combining smart contracts, API gating, and a user-friendly frontend.

**Problem**: DeFi infrastructure has no standard way to monetize via micropayments
**Solution**: Credit-based execution system enforced on-chain and via HTTP 402

### How It Works

1. **Buy Credits**: Pay MNEE tokens → receive on-chain credits (1 MNEE = 1 swap)
2. **Execute Swaps**: Credits checked by API and smart contract before execution
3. **Auto Refund**: Failed swaps automatically refund credits

## ✨ Features

- 💳 **Pay-per-use**: 1 MNEE = 1 swap credit
- 🚨 **HTTP 402 Gating**: API returns "Payment Required" when credits depleted
- 🔄 **1inch Integration**: Best swap rates via DEX aggregator
- 💸 **Auto Refunds**: Credits returned if swap fails
- 🔗 **Dual Wallet Support**: RainbowKit + thirdweb
- ⚡ **Gas Optimized**: Target <200k gas per swap

## 🏗️ Architecture

```
Frontend (Next.js + wagmi + RainbowKit)
    ↓ HTTP/JSON-RPC
API Routes (/api/prepare-swap → returns 402 or swap data)
    ↓ JSON-RPC
Smart Contracts (Sepolia)
    ├─ CreditManager (purchase/consume/refund credits)
    ├─ SwapExecutor (execute swaps with credit gate)
    └─ 1inch Router (DEX aggregation)
```

## 🛠️ Tech Stack

- **Contracts**: Solidity 0.8.20 + Foundry
- **Backend**: Next.js 15 API Routes + viem
- **Frontend**: React 19 + wagmi + RainbowKit + thirdweb + Tailwind CSS
- **Network**: Ethereum Sepolia Testnet
- **Integration**: 1inch API v6.0

## 🚀 Quick Start

### Prerequisites

- Node.js 18+, pnpm, Foundry, MetaMask

### Installation

```bash
# Clone repo
git clone https://github.com/vyqno/pay-per-defi-execution.git

cd mnee-01

# Install dependencies
pnpm install
cd smart-contracts && forge install && cd ..

# Configure environment
cp .env.example .env.local
# Edit .env.local with your API keys and RPC URLs

# Run development server
pnpm dev
```

## 📂 Project Status

**Current Phase**: Smart Contract Development

### To-Do
- [ ] Write CreditManager.sol contract
- [ ] Write SwapExecutor.sol contract
- [ ] Write MockMNEE.sol test token
- [ ] Create comprehensive test suite
- [ ] Implement API routes (/api/quote, /api/prepare-swap)
- [ ] Build frontend components
- [ ] Deploy to Sepolia testnet

### Contracts (Planned)

**CreditManager.sol** - Credit system management
- `purchaseCredits()` - Buy credits with MNEE
- `consumeCredit()` - Use credit for swap
- `refundCredit()` - Return credit on failure

**SwapExecutor.sol** - Swap execution with gating
- `executeSwap()` - Execute 1inch swap if credits available

**MockMNEE.sol** - Test token for Sepolia
- `faucet()` - Mint test MNEE

## 📁 Project Structure

```
smart-contracts/       # Foundry contracts (to be implemented)
src/
  ├── app/            # Next.js app router
  ├── components/     # React components (to be built)
  └── lib/            # Utilities & configs
.env.local           # Environment configuration
```

## 📝 Development

```bash
# Smart contracts
cd smart-contracts
forge build
forge test

# Frontend
pnpm dev
```

## 🤝 Contributing

Open to contributions! This is an early-stage project implementing HTTP 402 for DeFi.

---

**Status**: 🚧 In Development | **Network**: Ethereum Sepolia Testnet

---
