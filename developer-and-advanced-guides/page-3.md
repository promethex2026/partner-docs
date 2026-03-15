# Partner Integration Guide

This guide covers the three ways to integrate PrometheX prediction markets into your platform, with a detailed breakdown of the **White-Label deployment** — the most common path for partners.

---

## Integration Modes

| Feature | White-Label | Embedded Widget | API-Only |
|---|:-:|:-:|:-:|
| **Time to launch** | 1--2 weeks | 1--3 days | 4--8 weeks |
| **Engineering effort** | None (config only) | Low (embed code) | High (full build) |
| **UI customization** | Theme + branding | Widget styling | Complete control |
| **Custom domain** | Yes -- `markets.yoursite.com` | No -- hosted widget | N/A |
| **Feature flags** | Yes -- full control | Yes -- widget-level | N/A |
| **Trading UI** | Included | Included | Build your own |
| **User auth** | Privy (managed) | Privy (managed) | Your own + API keys |
| **Gasless transactions** | Included | Included | Via UserOp API |
| **Real-time data** | SSE built-in | SSE built-in | SSE subscription |
| **Admin dashboard** | Full access | Full access | Full access |
| **Community features** | Posts, comments | Configurable | Build your own |
| **Ideal for** | Fast launch, non-technical teams | Adding markets to existing app | Unique UX requirements |

### Which Model Should I Choose?

**I want to launch fast with my own brand**

Choose White-Label. You get a production-ready prediction market under your brand in 1--2 weeks. We configure your tenant (domain, theme, features, fees), and you're live. No frontend code, no backend work. Best for: crypto platforms, media companies, and communities that want to ship prediction markets without building anything.

**I want to add markets to my existing app**

Choose Embedded. Drop a market widget into your current product with a few lines of code. Users can browse and trade prediction markets without leaving your app. Best for: news apps, social platforms, and gaming sites that want to enrich their product with prediction markets as a feature.

**I want complete control over UX**

Choose API-Only. Use the PrometheX REST API to fetch markets, execute trades, and manage positions -- then build whatever UI you want. You control every pixel. Best for: trading platforms, DeFi protocols, and teams with strong frontend engineering who want a bespoke experience.

**I'm not sure yet**

Start with Embedded, upgrade to White-Label or API-Only later. The underlying API and smart contracts are the same across all models. You can embed a widget today and migrate to a full white-label deployment when you're ready.

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
| **Fee structure** | 1%--5% per trade | Configurable per market at creation |

### Detailed Configuration

White-Label deployments are configured through the Admin Dashboard. No code changes required.

#### Branding

| Setting | Description | Example |
|---|---|---|
| `tenant.name` | Display name | "AcmeMarkets" |
| `tenant.domain` | Custom domain | `markets.acme.com` |
| `tenant.logo` | Logo URL (light + dark variants) | `https://acme.com/logo.svg` |
| `tenant.colors.primary` | Primary brand color | `#6366F1` |
| `tenant.colors.background` | Background color | `#0D0B1A` |
| `tenant.favicon` | Browser favicon | `https://acme.com/favicon.ico` |

#### Feature Flags

| Flag | Default | Description |
|---|:-:|---|
| `features.trading` | `true` | Enable buy/sell trading UI |
| `features.community` | `true` | Enable posts, comments, likes |
| `features.gamification` | `true` | Enable leaderboards, tasks, rewards |
| `features.inviteSystem` | `true` | Enable referral invite codes |
| `features.notifications` | `true` | Enable push notifications |
| `features.marketCreation` | `false` | Allow tenant admins to create markets |

#### Fee Structure

| Parameter | Default | Description |
|---|:-:|---|
| `fees.tradingFee` | 100 (1%) | Trading fee in basis points |
| `fees.platformShare` | 50% | PrometheX share of trading fees |
| `fees.tenantShare` | 50% | Partner share of trading fees |

> **Note:** Fee splits are configurable per tenant agreement. Contact us for custom fee structures.

### Admin RBAC Roles

Each White-Label partner gets admin access scoped to their tenant. Roles follow RBAC:

| Role | Permissions |
|---|---|
| **Super Admin** | Full access (PrometheX team) |
| **Tenant Admin** | Full access within tenant scope |
| **Operator** | Market and content management |
| **Viewer** | Read-only analytics access |

### Launch Checklist

1. **Provide branding assets** -- Logo (SVG, light + dark variants), brand colors, favicon, and display name.
2. **Configure DNS** -- Point your custom domain (e.g., `markets.yoursite.com`) to the Cloudflare Workers deployment via CNAME.
3. **Review feature flags** -- Decide which features to enable: trading, community, gamification, notifications.
4. **Agree on fee structure** -- Confirm trading fee percentage and revenue split.
5. **Test on staging** -- Verify your branded deployment on Arbitrum Sepolia with test USDC.
6. **Go live** -- We promote your configuration to production. Your prediction market is live.

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

> For complete Widget SDK documentation, see our [Developer Docs](https://guide.promethex.market).

### Configuration Options

| Option | Type | Default | Description |
|---|---|---|---|
| `marketAddress` | `string` | **required** | On-chain market contract address |
| `tenantId` | `string` | **required** | Your tenant identifier |
| `apiKey` | `string` | **required** | API key for authentication |
| `theme` | `"light"` / `"dark"` | `"light"` | Widget color theme |
| `width` | `string` | `"100%"` | Widget width (px or %) |
| `height` | `number` | `600` | Widget height in pixels |
| `locale` | `string` | `"en"` | Language code (`en`, `zh`) |
| `hideHeader` | `boolean` | `false` | Hide the market title bar |
| `tradingEnabled` | `boolean` | `true` | Enable trading (set `false` for view-only) |
| `showChart` | `boolean` | `true` | Show the price history chart |
| `showOrderBook` | `boolean` | `false` | Show the order book (when CLOB is available) |

### Event Callbacks

Listen for user actions and state changes in the embedded widget.

| Event | Payload | Description |
|---|---|---|
| `onTradeComplete` | `{ marketAddress, optionIndex, amount, price, txHash }` | User completed a trade |
| `onMarketLoad` | `{ marketAddress, title, options, prices }` | Market data loaded |
| `onPriceUpdate` | `{ marketAddress, prices }` | Real-time price change |
| `onError` | `{ code, message }` | Error occurred in widget |
| `onAuthRequired` | `{}` | User needs to authenticate to trade |

### Widget Display Modes

The embedded widget supports multiple display modes:

- **Full Market** -- Complete market view with title, chart, options, and trading interface. Best for dedicated market pages.
- **Compact Card** -- Minimal card showing market title, current prices, and a trade button. Best for market lists and sidebars.
- **Price Ticker** -- Inline price display with sparkline chart. Best for embedding in articles and news feeds.
- **Market List** -- Scrollable list of multiple markets with filters. Best for market discovery pages.

---

## API-Only

For partners who want **full control** over the user experience and prefer to build their own frontend.

### You Build vs. We Provide

| You Build | We Provide |
|---|---|
| Frontend UI and UX | REST API for all operations |
| User authentication flow | Privy SDK or your own auth + API keys |
| Market browsing and search | Market listing and detail endpoints |
| Trading interface | Order placement and execution API |
| Position tracking | Position and P&L query endpoints |
| Real-time updates | SSE event stream for live data |
| Notifications | Notification query API |

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

### Rate Limits

| Endpoint Type | Rate Limit | Notes |
|---|:-:|---|
| Public reads (markets, prices) | 100 req/min | Per API key |
| Authenticated reads (positions, trades) | 60 req/min | Per user |
| Write operations (orders, claims) | 20 req/min | Per user |
| SSE connections | 5 concurrent | Per user |

> **Note:** Rate limits are enforced per tenant. If you need higher limits, contact us to discuss your use case.

> For the complete API reference and endpoint documentation, see our [Developer Docs](https://guide.promethex.market).

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

## Shared Infrastructure

Regardless of which integration model you choose, you get the same core infrastructure:

| Component | Description |
|---|---|
| **Same smart contracts** | All models use the same PredictionFactory, APMM engine, and resolution modules on Arbitrum. |
| **Same API endpoints** | REST API endpoints and SSE streams are identical. White-Label and Embedded just add a UI layer on top. |
| **Same Admin Dashboard** | Every tenant gets full access to the Admin Dashboard for market management, content, and user oversight. |
| **Same Gasless UX** | ERC-4337 account abstraction and Paymaster are available across all integration models. Users never pay gas. |

---

## Getting Started

Ready to integrate? Here's how to begin:

1. **Contact us** — Reach out via the [Contact page](../appendix-and-support/contact-and-technical-demos.md) or your partnership channel
2. **Technical scoping** — We assess your chain, token, wallet, and branding requirements
3. **Deployment** — We deploy and configure your platform (White-Label) or provide SDK/API access
4. **Go live** — Your first markets are created, seeded, and ready to trade

> See [Service Tiers](../business-and-partnership/service-tiers.md) for pricing and feature comparison across integration levels.
