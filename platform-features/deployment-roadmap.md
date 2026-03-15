# Deployment Roadmap

PrometheX public roadmap — what's live, what's next, and where we're headed.

## What's Live Now

PrometheX is fully functional on **Arbitrum Sepolia** with the complete end-to-end stack deployed and operational.

- **Trading UI** — Browse markets, buy/sell positions, track P&L, view price charts, and claim winnings.
- **APMM Engine** — Automated Prediction Market Maker with weighted constant-product pricing for N-outcome markets.
- **Smart Contracts** — PredictionFactory + Prediction clones deployed on Arbitrum Sepolia. Factory-clone pattern with OpenZeppelin upgradeability.
- **Gasless Trading** — ERC-4337 account abstraction with Paymaster. Users trade without holding ETH.
- **Social Login** — Privy authentication — email, Google, Twitter, Discord, and wallet login. Smart accounts created automatically.
- **Admin Dashboard** — Multi-tenant RBAC dashboard for market lifecycle management, content, and user administration.
- **Community** — Posts, comments, likes, reputation system, leaderboards, invite system, and task rewards.
- **Backend Services** — 4 microservices: Market Backend (BFF), Market Service, Block Listener, Recommendation Engine.

## Next Up (Q1-Q2 2026)

### Q1 2026 — Protocol Upgrade

The current sprint focuses on upgrading the on-chain protocol to the Conditional Token Framework and adding modular resolution.

| Feature | Description | Status |
| --- | --- | :---: |
| **CTF Migration** | Replace ERC20 Option tokens with Gnosis Conditional Tokens (ERC1155). Enables ecosystem compatibility with Polymarket and other CTF-based platforms. | In Progress |
| **APMM on CTF** | Adapt the APMM pricing engine to work with ERC1155 conditional token positions instead of ERC20 tokens. | In Progress |
| **Modular Resolution** | Deploy MultisigResolution module alongside UMA Oracle. Partners choose their resolution mechanism per market. | In Progress |
| **Block Listener CTF** | Index new CTF events: ConditionPreparation, PositionSplit, PositionsMerge, PayoutRedemption. | Planned |
| **Frontend Adaptation** | Update trading UI for CTF positions: split, merge, redeem flows. | Planned |

### Q1 2026 — CLOB Integration

The Central Limit Order Book matching engine is built and ready for integration.

| Feature | Description | Status |
| --- | --- | :---: |
| **CLOB Match Engine** | RBTree order book, CTF position matching, Kafka event streaming, WAL + snapshots for durability. | Built |
| **Hybrid Router** | Smart order router that splits trades between APMM (passive liquidity) and CLOB (active market makers) for optimal execution. | Planned |
| **Backend Integration** | Connect match engine to Market Service and on-chain settlement via gRPC. | Planned |
| **Maker/Taker Fees** | Separate fee tiers for limit orders (maker) and market orders (taker). | Planned |

### Q2 2026 — Mainnet & Commercialization

Prepare the platform for production deployment and partner onboarding.

| Feature | Description | Status |
| --- | --- | :---: |
| **Smart Contract Audit** | Third-party security audit of all core contracts (Factory, Prediction, CTF, Resolution). | Planned |
| **Arbitrum One Deployment** | Deploy all contracts to Arbitrum mainnet with real USDC. | Planned |
| **Partner Onboarding** | Tier configurations, feature flags, guided deployment playbook, partner landing page. | Planned |
| **Embed SDK** | JavaScript and React SDK for embedded market widgets. npm packages with TypeScript types. | Planned |
| **Documentation** | Complete API reference, integration guides, and contract documentation. | In Progress |

## On the Horizon (H2 2026+)

| Feature | Description | Status |
| --- | --- | :---: |
| **Multi-Chain** | Deploy to Base, Polygon, and additional L2s based on partner demand. | Roadmap |
| **SDK Libraries** | Python and Go SDKs for server-side integration. | Roadmap |
| **Advanced Analytics** | Partner-facing analytics dashboard with volume, user engagement, and market performance metrics. | Roadmap |
| **Programmatic Markets** | API-driven market creation with configurable templates for recurring events (sports seasons, elections). | Roadmap |

## How We Prioritize

1. **Partner demand** — Features that unblock partner integrations and revenue take priority. If a partner needs it to launch, it moves up.
2. **Protocol completeness** — CTF migration, modular resolution, and CLOB integration complete the core protocol. These are non-negotiable before mainnet.
3. **Security** — Audit and security hardening gate mainnet deployment. No shortcuts.
4. **Developer experience** — SDKs, documentation, and embed widgets reduce partner integration time. Lower friction means faster partner adoption.

---

> This roadmap is updated regularly. Timelines are targets, not commitments — they shift based on engineering progress and partner feedback. Last updated: February 2026.
