# Partner Integration Guide

This guide covers the three ways to integrate PrometheX prediction markets into your platform, with a detailed breakdown of the **White-Label deployment** — the most common path for partners.

---

## Integration Modes

| Mode | What You Get | Control Level | Best For |
|------|-------------|---------------|----------|
| **White-Label** | Full turnkey platform — your brand, your domain | Highest | Partners who want the fastest time-to-market |
| **Embedded Widget** | Drop-in components for your existing app | Medium | Partners with an established product |
| **API-Only** | Raw API access — build your own frontend | Full customization | Partners with engineering teams who want complete control |

> **Not sure which to choose?** Most partners start with White-Label. You can always add API-Only or Widget integrations later.

---

## White-Label Deployment

The White-Label deployment gives you a complete, branded prediction market platform — ready to operate from Day 1.

### What You Receive

| Component | Description |
|-----------|-------------|
| **Trading App** | Consumer-facing web application under your brand, domain, and language |
| **Admin Dashboard** | Full back-office for market management, content control, user oversight, and analytics |
| **Smart Contracts** | Complete contract suite deployed to your chosen chain |
| **Backend Services** | API server, business logic engine, blockchain event listener, real-time push (SSE) |
| **Operations Support** | Market creation, settlement execution, liquidity management, 24/7 monitoring |

### Customization Options

| Area | Standard Configuration | Customizable To |
|------|----------------------|-----------------|
| **Blockchain** | Arbitrum | Any EVM chain (BSC, Base, Polygon, etc.) |
| **Collateral token** | USDC | Any standard ERC-20 token (automatic decimal handling) |
| **Wallet** | Privy embedded wallet (social login + AA) | WalletConnect (MetaMask, TokenPocket, etc.) |
| **Language** | English | Multi-language built-in (Chinese, Spanish, etc.) |
| **Branding** | PrometheX default | Your logo, colors, domain, and visual identity |
| **Market categories** | All 13 categories | Select categories relevant to your audience |
| **Fee structure** | 1%–5% per trade | Configurable per market at creation |

### Deployment Process

The typical White-Label deployment follows four milestones:

```mermaid
---
config:
  look: handDrawn
  theme: neutral
---
flowchart LR
    M1["M1\nContracts Ready"] --> M2["M2\nBackend & Admin Live"]
    M2 --> M3["M3\nFrontend Configured"]
    M3 --> M4["M4\nLaunch & Handover"]
```

**Milestone 1 — Contracts Ready**
- Smart contracts deployed and verified on target chain
- Collateral token compatibility validated
- Factory, oracle, and settlement contracts operational

**Milestone 2 — Backend & Admin Live**
- Backend microservices deployed (API + business logic + blockchain listener)
- Admin dashboard accessible
- Wallet integration configured and tested

**Milestone 3 — Frontend Configured**
- White-label app deployed with partner branding
- Domain and SSL configured
- End-to-end trading flow verified (deposit → trade → settle → claim)

**Milestone 4 — Launch & Handover**
- Admin team trained on market creation and operations
- Initial markets created and seeded with liquidity
- Monitoring and alerting in place
- Formal acceptance and handover

### What You Need to Provide

To kick off a White-Label deployment, we need:

1. **Chain preference** — Which blockchain to deploy on
2. **Collateral token** — Token contract address and details (or USDC)
3. **Wallet preference** — Embedded (Privy) or external (WalletConnect)
4. **Brand assets** — Logo, color palette, domain name
5. **Language** — Primary language for the platform
6. **Market categories** — Which categories you plan to operate

---

## Embedded Widget

For partners who want to add prediction markets to an **existing** application without building a full platform.

### Available Components

- **MarketCard** — Compact market display with live pricing
- **BetPanel** — Full trading interface (buy/sell/position view)
- **MarketList** — Filterable market directory
- **WalletButton** — Connect/disconnect wallet with balance display

### Embed Options

| Method | Use Case |
|--------|----------|
| **React component** | React/Next.js applications |
| **Web Component** | Any HTML page or framework |
| **iframe** | Simplest integration — zero code changes |

### Quick Example (React)

```jsx
import { MarketCard } from '@promethex/widget-react';

function App() {
  return (
    <MarketCard
      marketId="0x..."
      theme="dark"
      onTrade={(result) => console.log(result)}
    />
  );
}
```

> For complete Widget SDK documentation, see our [Developer Docs](https://docs.promethex.market).

---

## API-Only

For partners who want **full control** over the user experience and prefer to build their own frontend.

### Capabilities

| Area | What You Can Do |
|------|----------------|
| **Markets** | List, filter, search, get details, create (with admin permissions) |
| **Trading** | Place buy/sell orders, query positions, check balances |
| **Liquidity** | Add/remove liquidity, query LP positions |
| **Resolution** | Submit outcomes, query settlement status, claim winnings |
| **Real-time** | Subscribe to SSE events (price changes, position updates, market status) |

### Authentication

- **Method:** Privy JWT (ES256 signature)
- **Flow:** Social login or wallet signature → JWT token → API access
- **AA support:** Optional ERC-4337 Account Abstraction for gasless user transactions

### Direct Contract Interaction

API-Only partners can also interact directly with on-chain contracts:

- **PredictionFactory** — Create markets programmatically
- **PredictionCTF** — Execute trades and manage liquidity
- **ConditionalTokens** — Split, merge, and redeem outcome tokens

Contract ABIs are available via the block explorer on each deployment chain.

> For the complete API reference and endpoint documentation, see our [Developer Docs](https://docs.promethex.market).

---

## Token Compatibility

If you plan to use a **custom ERC-20 token** as collateral (instead of USDC), it must meet these requirements:

| Requirement | Detail |
|-------------|--------|
| Standard interface | `transfer`, `approve`, `balanceOf` implemented correctly |
| Decimals | ≤ 18 |
| No fee-on-transfer | Token must not deduct fees on `transfer()` or `transferFrom()` |
| No rebase | Token supply must not change automatically |
| No blocklist risk | Token should not have centralized freeze/blocklist that could lock contract funds |

**If your token doesn't meet these requirements**, PrometheX provides a **WrappedCollateral** contract — a 1:1 ERC-20 wrapper that normalizes non-standard behavior.

We validate every custom token before deployment as part of the onboarding process.

---

## Getting Started

Ready to integrate? Here's how to begin:

1. **Contact us** — Reach out via the [Contact page](../appendix-and-support/contact-and-technical-demos.md) or your partnership channel
2. **Technical scoping** — We assess your chain, token, wallet, and branding requirements
3. **Deployment** — We deploy and configure your platform (White-Label) or provide SDK/API access
4. **Go live** — Your first markets are created, seeded, and ready to trade

> See [Service Tiers](../business-and-partnership/service-tiers.md) for pricing and feature comparison across integration levels.
