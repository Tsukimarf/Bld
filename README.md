# Token2025 — Web3

A smart contract deployment toolkit for ERC-20/EVM-compatible tokens, with MongoDB for off-chain data persistence.

---

## Overview

This module handles the full lifecycle of token and smart contract deployment on Ethereum and EVM-compatible networks. MongoDB is used to store deployment records, contract metadata, and transaction history off-chain.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Blockchain | Ethereum / EVM (Solidity) |
| Dev Framework | Hardhat / Ethers.js |
| Database | MongoDB |
| Language | JavaScript / Node.js |

---

## Prerequisites

- Node.js >= 16.x
- npm or yarn
- MongoDB (local or Atlas)
- MetaMask or a funded wallet with a private key
- An RPC endpoint (Infura, Alchemy, or local node)

---

## Installation

```bash
# Clone the repository
git clone https://github.com/Tsukimarf/Token2025.git
cd Token2025/web3

# Install dependencies
npm install
```

---

## Configuration

Create a `.env` file in the `web3/` directory:

```env
# Wallet
PRIVATE_KEY=your_wallet_private_key

# RPC
RPC_URL=https://mainnet.infura.io/v3/YOUR_PROJECT_ID

# MongoDB
MONGODB_URI=mongodb://localhost:27017/token2025

# Optional: Etherscan API for contract verification
ETHERSCAN_API_KEY=your_etherscan_api_key
```

> ⚠️ Never commit your `.env` file. It is already in `.gitignore`.

---

## Smart Contracts

Contracts are located in the `contracts/` directory. The main token contract follows the ERC-20 standard.

### Compile

```bash
npx hardhat compile
```

### Run Tests

```bash
npx hardhat test
```

### Deploy

```bash
# Deploy to local Hardhat network
npx hardhat run scripts/deploy.js --network localhost

# Deploy to a testnet (e.g. Sepolia)
npx hardhat run scripts/deploy.js --network sepolia

# Deploy to Ethereum mainnet
npx hardhat run scripts/deploy.js --network mainnet
```

Deployment records (contract address, transaction hash, block number, timestamp) are automatically saved to MongoDB after a successful deployment.

---

## Database (MongoDB)

MongoDB stores off-chain data related to deployments and contract state.

### Collections

| Collection | Description |
|---|---|
| `deployments` | Contract address, network, deployer, tx hash, timestamp |
| `tokens` | Token name, symbol, total supply, decimals |
| `transactions` | Historical on-chain interactions logged off-chain |

### Connect

Make sure MongoDB is running, then the app connects automatically via `MONGODB_URI` in your `.env`.

---

## Project Structure

```
web3/
├── contracts/          # Solidity smart contracts
├── scripts/            # Deployment and utility scripts
├── test/               # Contract tests
├── db/                 # MongoDB connection and models
├── hardhat.config.js   # Hardhat configuration
├── .env.example        # Environment variable template
└── README.md
```

---

## Networks

| Network | Chain ID | Notes |
|---|---|---|
| Hardhat (local) | 31337 | For development |
| Sepolia (testnet) | 11155111 | Recommended testnet |
| Ethereum Mainnet | 1 | Production |

---

## Contract Verification

After deploying to a public network, verify the contract on Etherscan:

```bash
npx hardhat verify --network sepolia DEPLOYED_CONTRACT_ADDRESS "Constructor Arg 1"
```

---

## License

MIT
