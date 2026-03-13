# API & SDK Overview

This page provides a high-level overview of the PrometheX developer toolkit — REST API, real-time events, Widget SDK, and smart contract interfaces. For complete endpoint documentation, refer to our [Developer Docs](https://docs.promethex.market).

---

## Platform API

The PrometheX API follows a standard REST pattern with JSON responses. All endpoints return:

```json
{
  "code": 0,
  "reason": "",
  "msg": "",
  "data": { ... }
}
```

### API Capabilities

| Domain | Operations |
|--------|-----------|
| **Markets** | List markets, get market details, filter by category/status, search, get hot/trending markets |
| **Trading** | Place buy orders (deposit), place sell orders (withdraw), query order history |
| **Positions** | Get user positions, get token balances, portfolio summary |
| **Liquidity** | Add liquidity, remove liquidity, query LP positions and rewards |
| **Resolution** | Submit market outcomes, query settlement status, claim winnings |
| **Users** | Get user profile, update settings, follow/unfollow, notifications |
| **Community** | Posts, comments, market discussions |
| **Leaderboard** | Trading volume rankings, profit rankings |

### Base URL

Each deployment has its own API endpoint, provided during onboarding:

```
https://api.{your-domain}/api/v1/
```

---

## Authentication

PrometheX uses **Privy** for authentication, supporting both social login and wallet-based auth.

### Auth Flow

```
User signs in (social or wallet) → Privy issues JWT → Client sends JWT with API requests
```

### Token Format

- **Type:** JWT (ES256)
- **Header:** `Authorization: Bearer <token>`
- **Expiry:** Managed by Privy SDK (auto-refresh)

### Account Abstraction (Optional)

For gasless user experiences, PrometheX supports **ERC-4337 Account Abstraction**:

- Users get a smart contract wallet (Light Account) automatically
- Transactions are sponsored via a Paymaster — users never need to hold gas tokens
- Compatible with all trading operations (buy, sell, claim, add/remove liquidity)

> AA can be enabled or disabled per deployment based on partner preference.

---

## Real-Time Events (SSE)

PrometheX provides **Server-Sent Events** for real-time data streaming — no WebSocket setup required.

### Available Event Streams

| Event | Payload | Use Case |
|-------|---------|----------|
| `market:price_change` | Market ID, new prices per outcome | Live price tickers |
| `market:info_update` | Volume, participant count, status changes | Market dashboards |
| `user:asset_changed` | Token balances | Wallet/portfolio display |
| `user:position_changed` | Position sizes, P\&L | Portfolio tracking |

### Connection Example

```javascript
const eventSource = new EventSource(
  'https://api.your-domain.com/api/v1/sse/connect',
  { headers: { 'Authorization': `Bearer ${token}` } }
);

eventSource.addEventListener('market:price_change', (event) => {
  const data = JSON.parse(event.data);
  console.log(`Market ${data.marketId}: YES=${data.prices.yes}`);
});
```

---

## Widget SDK

The Widget SDK provides ready-made UI components for embedding prediction markets into any web application.

### Packages

| Package | Description |
|---------|-------------|
| `@promethex/widget-core` | Framework-agnostic core library — API client, state management, types |
| `@promethex/widget-react` | React components — MarketCard, BetPanel, MarketList, WalletButton |

### Integration Methods

**React Component:**
```jsx
import { MarketCard, BetPanel } from '@promethex/widget-react';

<MarketCard marketId="0x..." theme="dark" />
<BetPanel marketId="0x..." onTradeComplete={handleTrade} />
```

**Web Component (any HTML page):**
```html
<script src="https://cdn.promethex.market/widget.js"></script>
<promethex-market-card market-id="0x..." theme="dark" />
```

**iframe (zero code changes):**
```html
<iframe
  src="https://app.your-domain.com/embed/market/0x..."
  width="400"
  height="600"
  frameborder="0"
/>
```

### Theming

Widgets support full visual customization:
- Light / dark mode
- Custom accent colors and fonts
- Responsive sizing
- Locale and language settings

---

## Smart Contract Integration

For partners using the **API-Only** mode or building custom frontends, direct contract interaction is available.

### Key Contracts

| Contract | Primary Functions |
|----------|-----------------|
| **PredictionFactory** | `createEvent()`, `createMarket()` — Create events and deploy market pools |
| **PredictionCTF** | `buy()`, `sell()`, `addLiquidity()`, `removeLiquidity()` — Core trading operations |
| **ConditionalTokens** | `splitPosition()`, `mergePositions()`, `redeemPositions()` — Token operations |
| **CTFSettlement** | `matchOrders()` — CLOB order matching (operator only) |
| **CTFRouter** | `depositAndSplit()`, `mergeAndRedeem()` — Convenience wrappers for multi-step operations |

### Getting Contract ABIs

- **Block explorer:** Verified source code and ABI available on Arbiscan (or equivalent for your chain)
- **On request:** We provide ABI JSON files as part of the integration package

### Reading On-Chain Data

All market state is queryable directly from the blockchain:
- Market parameters, reserves, and weights via `PredictionCTF`
- Token balances via `ConditionalTokens` (ERC-1155 `balanceOf`)
- Market metadata via `PredictionFactory`

---

## Market Maker Integration

For professional market makers looking to provide liquidity via the CLOB:

### Data Access

| Data | Source |
|------|--------|
| **Market prices** | REST API or SSE real-time stream |
| **Order book depth** | REST API (per market) |
| **Trade history** | REST API (filterable by market, time range) |
| **Position data** | REST API (authenticated, per user) |

### Order Submission

CLOB orders use **EIP-712 typed signatures**:

1. Construct the order (market, side, price in basis points, size, nonce, expiry)
2. Sign with EIP-712 using the maker's private key
3. Submit via API — the operator matches and settles on-chain

### APMM Parameters for Strategy

Market makers can query APMM state to inform their CLOB strategy:
- Current reserves and weights → implied APMM price
- Fee rate → minimum profitable spread
- Pool depth → expected slippage for APMM trades

---

## Full Documentation

For complete technical documentation including endpoint specifications, request/response schemas, error codes, and integration tutorials:

**[Developer Docs →](https://docs.promethex.market)**

The Developer Docs cover:
- Complete API Reference with request/response examples
- Smart Contract Reference with function signatures and events
- Widget SDK API with props, callbacks, and theming guide
- Integration tutorials and sample code
- Webhook and event documentation
