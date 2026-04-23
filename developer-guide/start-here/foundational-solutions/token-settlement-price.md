---
description: Real-Time Token Prices Derived From Actual On-Chain Swaps
---

# Token Settlement Price

## Overview

In DeFi, the price you see is not always the price you get. Traditional price services typically aggregate data from centralized exchanges, blend prices across multiple blockchain networks, and output a single averaged number. While convenient, this approach has real limitations: the averaged price often does not reflect the actual liquidity conditions on the specific chain where you intend to trade. The result can be unexpected slippage, less favorable rates, or a misleading view of a token's true market value on a given network. This problem is especially pronounced for less common tokens, tokens with uneven liquidity across chains, or fast-moving markets where conditions shift between the time a price is fetched and a trade is executed.

**The solution**

Token Settlement Price takes a fundamentally different approach. Instead of estimating or averaging, it derives prices directly from real swap transactions on the blockchain. Every time tokens are traded on a supported decentralized exchange (DEX), the system records the exact exchange ratio as the settlement price — the actual rate at which the trade was completed on-chain. These individual settlement prices are then organized into a comprehensive price graph spanning all supported DEX liquidity sources. From this graph, the system generates stable settlement prices — expressing every token's value in stablecoin terms (such as USDT or USDC) — updated with every new block on the blockchain.

Consequently, users gain access to token pricing that is transparent, verifiable, and grounded in what is actually happening on-chain. Settlement prices power the token price charts on [KyberSwap.com](http://kyberswap.com) and enable KyberSwap to measure token price volatility - giving users a more accurate and trustworthy view of market conditions to support their trading decisions.

{% hint style="info" %}
Note: Prices are tracked by KyberSwap from on-chain settlement data, calculated from actual swap events across supported DEX liquidity sources — not aggregated feeds or oracle data. Values may differ from prices on other platforms.
{% endhint %}

## Key Benefits

**Grounded in real trades, not estimates:** Every settlement price comes from an actual swap that was executed and settled on-chain. There is no modeling, no blending of unrelated markets — just the real exchange ratio from a completed transaction. This means the price data reflects genuine market activity, not theoretical calculations.

**Fully on-chain and verifiable:** Because the data originates from blockchain swap events, every settlement price can be traced back to the specific transaction and block where it occurred. This level of transparency is not possible with price feeds sourced from centralized exchanges or proprietary aggregation formulas.

**Network-specific accuracy:** Settlement prices are recorded per blockchain network. A token's price on Ethereum may differ from its price on Polygon, Arbitrum, or BSC due to differences in liquidity depth and trading activity. Settlement prices capture these network-specific conditions rather than blending them into a single cross-chain average that may not reflect reality on any individual chain.

**Broad token coverage:** The system processes swap events across 420+ liquidity sources on 17 supported chains, enabling settlement price tracking even for less common or exotic tokens that traditional price services may not cover well.

**Powers the features you use:** Settlement prices are the data behind the token price charts displayed on the KyberSwap interface, giving users a visual history of how a token's price has moved based on real trades.

## How It Works

Token Settlement Price operates as a three-stage data pipeline: capturing real swap data, computing prices, and building a structured price graph.

**Capturing swap events**

Every swap on a supported DEX liquidity source generates an on-chain event that records the tokens involved and the exact amounts exchanged. KyberSwap's system continuously ingests these swap events across all supported protocols and chains, normalizing data from different DEX formats into a consistent structure.

**Computing settlement prices**

For each swap, the settlement price is calculated as the direct ratio between the output amount and the input amount. For example, if a user swaps 1 ETH and receives 3,000 USDT, the settlement price of ETH in that transaction is 3,000 USDT.

To express a token's price in stablecoin terms (such as USDT), the system finds a pricing path through the price graph — for example, Token A → Token B → Token C → USDT. Not all paths are equal, so the system applies a set of priorities to select the most reliable one:

* **Shorter paths and legitimate hops.** Prefer fewer hops between tokens, routing through well-established tokens.
* **Higher-liquidity pools.** Prefer high-liquidity pools over small ones.
* **Recent swaps.** Only include swaps within a 1-day window.
* **Larger trade sizes.** Prefer big swaps over tiny ones.

The system applies these priorities progressively, starting with the strictest criteria — for example, a maximum of 3 hops, hops through top 100 tokens, swaps within the last 15 minutes, and a minimum swap amount of $10 USD. If a price can be found under these conditions, that price is used. Otherwise, the system gradually relaxes the constraints until a price can be determined.

**Building the price graph**

Individual settlement prices are organized into a price graph — a network of token-pair price relationships across thousands of liquidity pools. On the Ethereum network alone, this graph spans approximately 16,000 tokens and 22,000 trading pairs. The graph is maintained in memory for fast access, synchronized to a caching layer for real-time retrieval, and archived in a time-series database for historical analysis.

From this graph, the system generates **stable settlement prices**: the value of every supported token expressed in a stablecoin. It achieves this by finding the most reliable pricing route from each token to a stablecoin, selecting from the top-ranked liquidity pools. These stable prices are updated on a per-block basis, ensuring they stay current with the latest on-chain activity.

#### Reliability and Data Integrity

Blockchain networks can occasionally experience temporary forks - known as reorganizations - where a set of recently confirmed blocks is replaced by an alternative chain. Because settlement prices are derived from individual, independent swap events rather than accumulated over time, the system handles this cleanly: it removes any prices associated with the reorganized blocks and recalculates from the corrected chain state. This design ensures that the pricing data remains accurate and consistent, even when the underlying blockchain undergoes unexpected changes.

#### Token Settlement Price vs. On-Chain Price Service

KyberSwap provides two distinct pricing solutions, each serving a different purpose:

* **Token Settlement Price** captures the actual exchange rate from every completed swap on supported DEX liquidity sources. It is backward-looking — recording what happened in real, on-chain transactions. Settlement prices power the token price charts on [KyberSwap.com](http://kyberswap.com) and enable KyberSwap to measure token price volatility.
* [**On-Chain Price Service**](kyberswap-onchain-price-service.md) delivers accurate, reliable, and tradeable price information for a wide array of tokens. It leverages the same route-finding algorithm used in KyberSwap's token swap calculations (`CalcAmountOut`) to ensure consistency and precision in price determination. It is forward-looking — estimating what you would get if you swapped right now, based on current on-chain liquidity.

<table data-header-hidden><thead><tr><th width="197.90234375"></th><th></th><th></th></tr></thead><tbody><tr><td></td><td><strong>Token Settlement Price</strong></td><td><strong>On-Chain Price Service</strong></td></tr><tr><td>What it does</td><td>Records the actual price from every completed swap</td><td>Calculates real-time tradeable prices via route simulation</td></tr><tr><td>Source of price</td><td>DEX swap events on-chain</td><td>DEXs using multiple pairs with different quote tokens</td></tr><tr><td>Price formula</td><td>Direct ratio: <code>amountOut / amountIn</code> from completed swaps</td><td>Graph-based algorithm using <code>CalcAmountOut</code>: buy price = <code>maximum output amount</code>; sell price = <code>minimum input amount</code></td></tr><tr><td>Price direction</td><td>Backward-looking — what happened</td><td>Forward-looking — what would happen now</td></tr><tr><td>Buy/Sell distinction</td><td>Single price per swap</td><td>Separate buy and sell prices</td></tr><tr><td>Update frequency</td><td>Per swap event, per block</td><td>Every ~10 seconds</td></tr><tr><td>Quote denomination</td><td>Stablecoins (via stable settlement prices)</td><td>Stablecoins (USDT, USDC) and native tokens (ETH, BNB, etc.)</td></tr><tr><td>Used for</td><td>Token price charts, volatility measurement</td><td>Up-to-date and tradeable price information via API</td></tr></tbody></table>

Together, they provide users with both a historically grounded view of token prices and forward-looking, actionable pricing for trading decisions.

## Frequently Asked Questions

**How is settlement price different from the token price I see on CoinGecko or CoinMarketCap?**

Services like CoinGecko and CoinMarketCap typically aggregate prices from both centralized and decentralized exchanges across multiple chains, then blend them into a single average. Settlement price is derived solely from on-chain swap events on a specific network. This means it more accurately reflects the actual liquidity and trading conditions on the chain where you plan to trade, but values may differ from those platforms.

**Why does the same token have different prices on different blockchain networks?**

Liquidity depth and trading activity vary across blockchain networks. A token may have deep liquidity on Ethereum but thinner liquidity on Arbitrum or Polygon, leading to different effective prices. Settlement prices capture these per-network differences because they are recorded from real swaps on each chain individually, rather than averaged into a single cross-chain number.

**How often are settlement prices updated?**

Settlement prices are recorded with every new swap event on every new block. The stable settlement prices derived from them are also updated on a per-block basis, ensuring the data stays current with the latest on-chain activity.

**Does settlement price cover low-liquidity or newly listed tokens?**

Yes. Because settlement prices are generated from swap events across supported liquidity sources on [our supported chains](../../../getting-started/supported-exchanges-and-networks.md), even less common or newly listed tokens receive price data as soon as they are tradeable on supported DEX liquidity sources.

**Why might KyberSwap's token price differ from other platforms?**

KyberSwap tracks prices from on-chain settlement data calculated from actual swap events — not from aggregated feeds or oracle data. Other platforms may aggregate prices from centralized exchanges, combine data across multiple chains, or use different calculation methods. These differences in methodology and data sources can result in price variations between platforms.
