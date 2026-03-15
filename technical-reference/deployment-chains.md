# Deployment & Chains

This page covers supported blockchain networks, staging environment details, and how to get started with PrometheX infrastructure.

---

## Supported Chains

### Current Support

PrometheX smart contracts are deployed on **Arbitrum** — an Ethereum Layer 2 rollup that provides low gas costs, fast finality, and full EVM compatibility. All PrometheX contracts, trading, and settlement happen on-chain on Arbitrum.

**Arbitrum Sepolia (Testnet) — Live now.**
Full platform deployment for development, testing, and partner onboarding. Uses test USDC (tUSDC) with no real value at stake.

| Property | Value |
|----------|-------|
| **Network** | Arbitrum Sepolia |
| **Chain ID** | `421614` |
| **Currency** | ETH (Sepolia) |
| **Base Token** | Test USDC (tUSDC) — 6 decimals |
| **RPC Endpoint** | `https://sepolia-rollup.arbitrum.io/rpc` |
| **Block Explorer** | [sepolia.arbiscan.io](https://sepolia.arbiscan.io/) |
| **Avg Block Time** | ~250ms |
| **Finality** | ~15 minutes (L1 confirmation) |
| **Status** | Active |

**Arbitrum One (Mainnet) — Planned Q2 2026.**
Production deployment for live markets with real USDC. Launching after staging validation and audit completion.

| Property | Value |
|----------|-------|
| **Network** | Arbitrum One |
| **Chain ID** | `42161` |
| **Currency** | ETH |
| **Base Token** | USDC ([`0xaf88d065e77c8cC2239327C5EDb3A432268e5831`](https://arbiscan.io/address/0xaf88d065e77c8cC2239327C5EDb3A432268e5831)) |
| **Block Explorer** | [arbiscan.io](https://arbiscan.io/) |
| **Avg Block Time** | ~250ms |
| **Finality** | ~15 minutes (L1 confirmation) |
| **Status** | Planned — Q2 2026 |

> **Note:** Mainnet deployment is contingent on successful staging validation, completion of the CTF protocol upgrade, and smart contract audit.

### Why Arbitrum?

| Factor | Benefit |
|--------|---------|
| **Low gas costs** | Trades cost fractions of a cent — critical for micro-markets and frequent trading |
| **Fast finality** | Sub-second block times on L2, with L1 finality in ~15 minutes |
| **EVM compatible** | Standard Solidity contracts, no custom VM or language |
| **Ecosystem** | Large DeFi ecosystem including UMA Oracle, Alchemy AA, and native USDC |
| **Security** | Inherits Ethereum L1 security through rollup proofs |
| **Adoption** | Highest TVL among Ethereum L2s, strong developer community |

### Multi-Chain Roadmap

PrometheX smart contracts are chain-agnostic — the factory-clone pattern and APMM engine work on any EVM chain. Multi-chain expansion is planned after Arbitrum mainnet launch.

| Phase | Network | Timeline | Notes |
|-------|---------|----------|-------|
| **Current** | Arbitrum Sepolia | Live | Full staging environment |
| **Next** | Arbitrum One | Q2 2026 | Mainnet launch |
| **Future** | Base | H2 2026 | Coinbase ecosystem, high growth |
| **Future** | Polygon | H2 2026 | Low cost, large user base |
| **Evaluating** | Additional L2s | 2027+ | Based on partner demand |

> **Note:** Multi-chain deployment is driven by partner demand. If your use case requires a specific chain, contact [tech@PrometheX.market](mailto:tech@PrometheX.market) to discuss priorities.

### Adding a Custom Network

For partners with specific chain requirements, PrometheX can deploy to any EVM-compatible network. The deployment process involves:

1. **Contract deployment** — Deploy PredictionFactory and supporting contracts to the target chain
2. **Oracle configuration** — Set up resolution module (UMA availability varies by chain; multisig works everywhere)
3. **Base token whitelisting** — Configure the accepted stablecoin (USDC, USDT, etc.)
4. **Infrastructure setup** — Configure Block Listener, RPC endpoints, and bundler for the target chain
5. **Testing** — Full integration test on the target chain's testnet

---

## Staging Environment

### Overview

The PrometheX staging environment is a fully functional deployment on Arbitrum Sepolia. Every feature available in production is available here — trading, market browsing, gasless transactions, real-time data, and admin tools.

| Property | Value |
|----------|-------|
| **App URL** | [app.promethex.market](https://app.promethex.market) |
| **API Base URL** | `https://app.promethex.market/api/v1` |
| **Network** | Arbitrum Sepolia |
| **Chain ID** | `421614` |
| **RPC Endpoint** | `https://sepolia-rollup.arbitrum.io/rpc` |
| **Block Explorer** | [sepolia.arbiscan.io](https://sepolia.arbiscan.io/) |

### Core Contracts on Staging

| Contract | Address | Explorer |
|----------|---------|----------|
| **PredictionFactory** (Proxy) | `0x2c3E6717C1CC3787dBf420985188e2562F1aE62B` | [View on Arbiscan](https://sepolia.arbiscan.io/address/0x2c3E6717C1CC3787dBf420985188e2562F1aE62B) |
| **MockOptimisticOracleV3** | `0xD72b4002c472B7084A5A2D21450Ad8092b8E2FF6` | [View on Arbiscan](https://sepolia.arbiscan.io/address/0xD72b4002c472B7084A5A2D21450Ad8092b8E2FF6) |
| **Test USDC (tUSDC)** | `0x934E616cA9538397E3f9a12895C40ea2E8C45E48` | [View on Arbiscan](https://sepolia.arbiscan.io/address/0x934E616cA9538397E3f9a12895C40ea2E8C45E48) |
| **ERC-4337 EntryPoint** | `0x5FF137D4b0FDCD49DcA30c7CF57E578a026d2789` | [View on Arbiscan](https://sepolia.arbiscan.io/address/0x5FF137D4b0FDCD49DcA30c7CF57E578a026d2789) |

### Getting Started

1. **Open the staging app** — Navigate to [app.promethex.market](https://app.promethex.market) in your browser.
2. **Sign in** — Click **Connect** and sign in with email, Google, Twitter, or an external wallet. Privy creates a smart account for you automatically — no wallet setup needed.
3. **Get test USDC** — Use the in-app faucet to receive tUSDC, or mint directly from the [tUSDC contract](https://sepolia.arbiscan.io/address/0x52cb113e383c654fB78Ff56615ce3719193C6408). Test tokens have no real value.
4. **Browse markets** — Explore active prediction markets. Each market shows current prices (probabilities), volume, and expiry date.
5. **Place a trade** — Select an outcome, enter your amount, and confirm. The trade executes on-chain with zero gas fees — the Paymaster covers everything.
6. **Monitor positions** — Track your open positions, P&L, and trade history in the portfolio view.

### Getting Testnet Tokens

#### Sepolia ETH

You only need Sepolia ETH if you plan to interact with contracts directly (not through the API). For gasless trading via the app or API, no ETH is required.

| Faucet | URL |
|--------|-----|
| QuickNode | [faucet.quicknode.com/arbitrum/sepolia](https://faucet.quicknode.com/arbitrum/sepolia) |
| Alchemy | [sepoliafaucet.com](https://sepoliafaucet.com/) |
| Arbitrum Bridge | Bridge Sepolia ETH via [bridge.arbitrum.io](https://bridge.arbitrum.io/) |

#### Test USDC (tUSDC)

| Method | Details |
|--------|---------|
| **In-app faucet** | Click the faucet button in the staging app after signing in |
| **Direct mint** | Call `mint()` on the [tUSDC contract](https://sepolia.arbiscan.io/address/0x52cb113e383c654fB78Ff56615ce3719193C6408) |

### API Access

The staging API is open for integration testing. All endpoints documented in the API Reference are available.

```bash
# List active markets
curl https://app.promethex.market/api/v1/market/get-markets?status=running

# Get market detail
curl https://app.promethex.market/api/v1/market/get-market-detail?marketAddress=0x...

# Subscribe to real-time events (SSE)
curl -N https://app.promethex.market/api/v1/sse/subscribe?channels=market:0x...
```

> **Note:** The staging environment uses the same API endpoints, authentication flow, and smart contracts as production. Code written against staging will work on mainnet with only a URL change.

### Infrastructure

The staging environment runs on dedicated infrastructure that mirrors the production topology:

| Component | Host | Details |
|-----------|------|---------|
| **Backend Services** | `54.179.181.210` | Docker Compose: Market Backend (8000), Market Service (9000), Recommendation (50051), Block Listener (8080) |
| **Admin Service** | `13.229.202.228` | Docker Compose: Admin App (8080), PostgreSQL, Redis, MinIO |
| **Frontend** | Cloudflare Workers | Edge-deployed React SPA |
| **Database** | PostgreSQL + pgvector | Markets, users, positions, embeddings |
| **Cache** | Redis | Rate limiting, locks, block tracking |
| **Storage** | MinIO (S3-compatible) | Images, assets |

### Limitations

The staging environment has a few differences from production:

| Area | Staging | Production |
|------|---------|------------|
| **Network** | Arbitrum Sepolia | Arbitrum One |
| **Token** | tUSDC (test, mintable) | USDC (real) |
| **Oracle** | MockOptimisticOracleV3 | UMA OptimisticOracleV3 |
| **Data** | Test markets, may be reset | Persistent |
| **SLA** | Best effort | Production SLA |

> **Note:** The staging environment may be reset periodically as we deploy new features. Test data (markets, positions, trades) may not persist across resets.
