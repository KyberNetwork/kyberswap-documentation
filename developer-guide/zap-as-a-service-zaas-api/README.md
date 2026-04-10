---
description: >-
  Introducing Zap as a Service API (ZaaS) and Liquidity Widget, streamlining
  decentralized liquidity provision. Effortlessly add liquidity with a single
  token for enhanced DeFi engagement.
---

# Zap as a Service (ZaaS) API

## Overview & Capabilities

ZaaS (Zap as a Service) API lets integrators add one-click liquidity provisioning to any app. Users can enter, exit, or migrate a concentrated liquidity position using **any token** — no manual ratio calculation, no separate swap-then-deposit flow. The API handles routing through the KyberSwap aggregator and pool internals to minimize price impact automatically.

**Base URL:** `https://zap-api.kyberswap.com/{chain}`

***

### What ZaaS API Can Do

* **Zap In** — Open a new concentrated liquidity position or increase an existing one using any ERC-20 token or the chain's native token as input. The API automatically swaps and deposits in the correct ratio for the chosen price range.
* **Zap Out** — Remove liquidity from a position and receive a single output token, in one transaction.
* **Zap Migrate** — Move liquidity from one pool to another (across DEXes or fee tiers) in a single transaction.
* **Any-token input** — Input tokens are not limited to the pool's token pair. Pass any ERC-20 (`0x...`) or native token (`0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE`).
* **Partner fee collection** — Integrators can attach a `feeAddress` and `feePcm` to any route request to collect a fee from the input token.
* **EIP-2612 Permit** — The `KSZapRouterPositionPermit` contract supports gasless approvals so users can skip a separate ERC-20 approval transaction.
* **Slippage protection** — All routes include minimum output and minimum liquidity thresholds; the contract reverts if on-chain conditions exceed the configured slippage tolerance.
* **Capital efficiency** — Fallback swaps are executed automatically if the first routing attempt leaves unused capital, maximising position size even in volatile markets.
* **14 supported chains** — Arbitrum, Avalanche, Base, BSC, Ethereum, Linea, Optimism, Polygon, Ronin, Scroll, Sonic, Berachain, zkSync, and more. See Supported Chains & DEXes.
* **55+ DEX integrations** — Uniswap V3/V4, PancakeSwap V3, Aerodrome, Velodrome, Camelot, SushiSwap, Curve, Balancer, and many others. See [DEX IDs](zaps-supported-chains-dexes.md).

***

### When to Use ZaaS API

ZaaS is aimed at **builders who want to add liquidity UX to their product** without implementing swap routing or pool math themselves:

| Audience                 | Use case                                                   |
| ------------------------ | ---------------------------------------------------------- |
| Wallet apps              | One-click "Earn" or "Add Liquidity" from any held token    |
| Portfolio managers       | Rebalance into an LP position without manual swaps         |
| DEX front-ends           | Compete on UX by abstracting away token ratio complexity   |
| Aggregators / meta-dexes | Bundle liquidity provision into a broader swap/invest flow |

***

### Endpoint Index

All endpoints share the base URL `https://zap-api.kyberswap.com/{chain}`. Pass your `X-Client-ID` header on every request.

| Method | Path                          | Description                                                         |
| ------ | ----------------------------- | ------------------------------------------------------------------- |
| `GET`  | `/api/v1/in/route`            | Preview the best Zap-In route for a given input and target position |
| `POST` | `/api/v1/in/route/build`      | Build the on-chain calldata for a Zap-In route                      |
| `GET`  | `/api/v1/migrate/route`       | Preview the best Zap-Migrate route from one pool to another         |
| `POST` | `/api/v1/migrate/route/build` | Build the on-chain calldata for a Zap-Migrate route                 |
| `GET`  | `/api/v1/out/route`           | Preview the best Zap-Out route for exiting a position               |
| `POST` | `/api/v1/out/route/build`     | Build the on-chain calldata for a Zap-Out route                     |

{% hint style="info" %}
**Rate limiting:** Without a whitelisted Client ID, requests are limited to **10 per 10 seconds**. Contact [business@kyber.network](mailto:business@kyber.network) to request a higher quota.
{% endhint %}

For full parameter and response schemas, see the [API Reference](api-reference/) section. For code examples, see the [How-to Guides](how-to-guides/).

