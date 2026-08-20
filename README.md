# 📈 Chainlink Price-Gated Disbursement Escrow

[![Polygon Amoy](https://img.shields.io/badge/Network-Polygon_Amoy-purple?logo=polygon)](#)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.24-lightgrey?logo=solidity)](https://soliditylang.org/)
[![Foundry](https://img.shields.io/badge/Framework-Foundry-orange)](https://getfoundry.sh/)
[![Chainlink](https://img.shields.io/badge/Oracles-Chainlink_Price_Feeds-blue?logo=chainlink)](https://chain.link)

> **Automated, price-hedged, and oracle-verified disbursement gateway for token payouts on Polygon using Chainlink Price Feeds.**

---

## 🌟 Executive Overview & Web3 Paradigm Aim

In Web3 token grants, structured donor campaigns, and financial milestones, applications face asset volatility issues:
1. **Token Volatility Risk**: Funding allocated for a specific real-world cause (e.g. food supplies, school infrastructure) can fluctuate in value before payout.
2. **Oracle-Verified Release Triggers**: Disbursing funds manually or trusting a centralized server to verify asset prices introduces security bottlenecks.

### The Plug-and-Play Solution: Chainlink Price-Gated Escrow
This repository provides a **price-gated escrow disbursement contract** integrated with **Chainlink Price Feeds**. Any campaign can lock funds in escrow and automatically release them to recipients (or trigger refunds) only when an asset (e.g., BTC/USD, ETH/USD) crosses a defined price threshold on-chain.

---

## 🔬 Key Web3 Technical Concepts & Architecture

### 1. Decentralized Oracle Price Aggregation
- **Chainlink Data Feeds**: Pulls real-time, tamper-proof asset price updates from highly decentralized node operators directly into the smart contract.
- **On-Chain Querying**: Instead of storing static prices, the contract fetches live rates using the `latestRoundData()` function, protecting the vault against central points of failure.

### 2. Time-Weighted Escrow and Safeguards
- Funds are safely held in the smart contract's custody until target price conditions are verified on-chain.
- Includes emergency rescue/refund thresholds if the target price is not met by a specific deadline.

### 3. Scalable Execution on Polygon L2
- Low transaction fees on Polygon ensure that checking oracle data and disbursing funds remains highly gas-efficient.

---

## 📍 Live On-Chain Deployments (Polygon Amoy Testnet)

| Contract | Network | Deployed Address | Block Explorer |
| :--- | :--- | :--- | :--- |
| **`PriceGatedEscrow`** | **Polygon Amoy** | *TBD (Pending Deployment)* | [View on PolygonScan](#) |

- **Deployment Tx Hash**: *TBD (Pending Deployment)*

---

## 🛠️ Project Architecture & Data Schema

```
02_polygon_chainlink_pricegated_disbursement/
├── README.md                               # Project documentation
├── .gitignore                              # Root git ignore file
├── contracts/
│   ├── src/
│   │   ├── interfaces/
│   │   │   └── AggregatorV3Interface.sol   # Chainlink Aggregator interface
│   │   ├── mocks/
│   │   │   └── MockV3Aggregator.sol        # Mock price feed for local testing
│   │   └── PriceGatedEscrow.sol            # Core disbursement logic
│   ├── test/
│   │   └── PriceGatedEscrow.t.sol          # Automated Forge test cases
│   ├── script/
│   │   └── Deploy.s.sol                    # Solidity deployment script
│   ├── foundry.toml                        # Forge compilation settings
│   └── .env                                # Protected deployment key storage
└── frontend/
    └── index.html                          # Glassmorphic Dapp gateway UI
```

### On-Chain Data Schema (`PriceGatedEscrow.sol`)
* `priceFeed`: Address of the Chainlink price aggregator contract.
* `targetPrice`: Target asset price threshold (scaled to feed decimals) required for disbursement.
* `recipient`: The address designated to receive the funds upon matching conditions.
* `disbursed`: Status flag to prevent double-spending or re-entry during payout.

---

## 🧰 Technology Stack

- **Smart Contracts**: Solidity `^0.8.24`
- **Development & Testing**: Foundry (`forge`, `cast`)
- **Oracle Integration**: Chainlink Price Feeds SDK (`AggregatorV3Interface`)
- **Blockchain Network**: Polygon Amoy Testnet (Chain ID `80002`)
- **Frontend Dapp**: Vanilla HTML5 / Modern CSS3 (Glassmorphism), Ethers.js `v6`

---

## 🚀 Quickstart & Local Setup

To easily set up this repository in standalone mode (configure environment files, install local dependencies, and compile contracts in one click), run:
```bash
chmod +x setup.sh
./setup.sh
```


### 1. Smart Contract Compilation & Unit Tests
```bash
cd contracts

# Compile Solidity contracts
forge build

# Run automated unit tests
forge test -vv
```

### 2. Deploying to Polygon Amoy
```bash
cd contracts

# Set environment variables:
# PRIVATE_KEY=your_private_key_here
# POLYGON_AMOY_RPC_URL=your_amoy_rpc_url_here

# Deploy the contract using Foundry script
forge script script/Deploy.s.sol:DeployScript --rpc-url $POLYGON_AMOY_RPC_URL --broadcast --verify -vvvv
```

### 3. Launching the Web Dapp
```bash
# Serve frontend folder via HTTP
cd frontend
python3 -m http.server 8002
```
Open **[http://localhost:8002](http://localhost:8002)** in Google Chrome, connect MetaMask to Polygon Amoy, and interact with the price-gated dashboard!

---

## 📜 License
MIT License. Built with ❤️ for the Polygon Ecosystem.
