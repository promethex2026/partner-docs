# APMM Engine & Pricing

PrometheX powers prediction markets with a purpose-built pricing engine — the **Automated Prediction Market Maker (APMM)** — combined with an optional **Central Limit Order Book (CLOB)** for professional liquidity. This section explains how it works and why it matters for your platform.

***

## Probability Tokenization

Every prediction market on PrometheX is backed by **Conditional Tokens** — an ERC-1155 standard originally developed by Gnosis.

**How it works:**

1. A user deposits **1 USDC** into a binary market (e.g., "Will BTC hit $100K?").
2. The system **splits** that 1 USDC into **1 YES token** and **1 NO token**, both held in the liquidity pool.
3. Token prices always sum to $1.00 — forming a natural probability distribution.
4. When the market resolves, winning tokens redeem **1:1** for the collateral. Losing tokens become worthless.

This **mint-and-burn** mechanism ensures the system is always fully collateralized — no counterparty risk, no fractional reserves.

> **Price = Probability.** If YES trades at $0.65, the market collectively estimates a 65% chance of that outcome occurring.

***

## Weighted Product Invariant

PrometheX uses a **weighted constant-product** formula to price outcomes automatically — no order book or market maker required on Day 1.

### The Core Formula

For a market with outcomes indexed by _i_, the invariant is:

```
∏ᵢ (rᵢ ^ wᵢ) = k   (constant)
```

Where:

* **rᵢ** = reserve (token balance) of outcome _i_
* **wᵢ** = weight assigned at market creation
* **k** = invariant constant, maintained across all trades

### Pricing

The instantaneous price of outcome _i_ is:

```
priceᵢ = 1 / Σⱼ (wⱼ / wᵢ × rᵢ / rⱼ)
```

**Configurable weights** allow market creators to set initial probabilities that reflect real-world expectations. For example, setting weights to 80/20 starts a market at $0.80 / $0.20 — appropriate for a heavy favorite.



***

## Hybrid Liquidity: APMM + CLOB

PrometheX offers a **hybrid liquidity model** — combining passive APMM liquidity with active CLOB order matching in the same market.

### Two Trading Channels

|                    | APMM Channel                    | CLOB Channel                       |
| ------------------ | ------------------------------- | ---------------------------------- |
| **Liquidity type** | Passive — always available      | Active — maker/taker orders        |
| **Pricing**        | Algorithmic (weighted product)  | Order-driven (limit orders)        |
| **Requirement**    | Initial liquidity deposit       | Market makers / active traders     |
| **Best for**       | Guaranteed liquidity from Day 1 | Price discovery at scale           |
| **Settlement**     | On-chain, atomic                | EIP-712 signed, operator-submitted |

### Configuration Per Market

Each market can be configured with one of three modes:

| Mode          | Flag | Use Case                                              |
| ------------- | ---- | ----------------------------------------------------- |
| APMM only     | `1`  | New markets, long-tail events                         |
| CLOB only     | `2`  | High-volume markets with active MMs                   |
| Hybrid (Both) | `3`  | Best of both — APMM baseline + CLOB price improvement |

In **hybrid mode**, the APMM provides a liquidity floor while the CLOB enables tighter spreads and better price discovery as volume grows.

### How PrometheX Compares

|                           | PrometheX            | Polymarket             | Azuro          |
| ------------------------- | -------------------- | ---------------------- | -------------- |
| **Pricing model**         | APMM + CLOB (hybrid) | CLOB only              | AMM only       |
| **Day 1 liquidity**       | Yes (APMM)           | Requires market makers | Yes (AMM pool) |
| **Professional trading**  | Yes (CLOB)           | Yes (CLOB)             | Limited        |
| **Weight customization**  | Yes                  | N/A                    | Limited        |
| **Multi-outcome markets** | Native (NegRisk)     | Yes                    | Limited        |

***

## Why This Matters for Partners

### Instant Liquidity — No Market Makers Required

With APMM, every market is tradeable the moment it goes live. No need to recruit market makers, negotiate deals, or subsidize order books. Deploy a market, seed initial liquidity, and trading begins immediately.

### Long-Tail Markets at Scale

Traditional order books struggle with niche markets — there simply aren't enough makers. APMM solves this by providing algorithmic liquidity for **any** market, no matter how obscure. This unlocks categories like regional elections, local sports, or industry-specific events.

### Configurable Fee Model

* **Fee range:** 1% – 5% per trade (configurable per market at creation)
* **Direction:** Collected on both buy and sell
* **Allocation:** 100% flows to liquidity providers
* **Cap:** 500 basis points maximum (enforced on-chain)

Partners earn revenue through the fee structure defined in their service tier. See [Revenue Model & Revenue Sharing](../business-and-partnership/revenue-model-and-revenue-sharing.md) for details.

### Predictable Economics

Because the APMM is fully on-chain and deterministic:

* **No hidden spreads** — pricing is transparent and verifiable
* **No counterparty risk** — collateral is locked in smart contracts
* **No market manipulation** — trades follow the invariant mathematically
* **Full auditability** — every trade is an on-chain transaction
