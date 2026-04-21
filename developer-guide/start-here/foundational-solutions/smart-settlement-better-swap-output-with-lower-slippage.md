---
description: Atomic Pools Comparison for Higher Swap Output with lower Slippage
---

# Smart Settlement

## Overview

Standard DEX aggregators determine the optimal swap route at quote time - before a transaction is submitted. While this works well under normal conditions, it leaves trades exposed to execution-time risks: liquidity shifts, front-running, and PropAMM operators who quote tight spreads to attract order flow before widening them at execution.\
\
Smart Settlement addresses this by extending KyberSwap Aggregator’s existing [Dynamic Trade Routing](dynamic-trade-routing.md) with an additional on-chain decision layer. At the moment of execution, Smart Settlement compares multiple candidate pools in real time and selects the one that delivers the highest token output for each swap hop. This comparison is atomic - it occurs within the same transaction, with no additional steps required from the user.\
\
The result is a swap execution that is more resilient to slippage, more resistant to PropAMM manipulation, and consistently closer to the quoted rate - regardless of market conditions at the time of submission.

## Key Benefits

* **More Tokens Received** - Real-time pool comparison finds the route that gives you the highest possible output.
* **Minimized Slippage** - On-chain decision making reduces the gap between quoted and received amounts.
* **Protection Against PropAMM Spoofing** - Proprietary AMMs (PropAMMs) are automated market makers operated by professional market makers who can dynamically adjust their pricing. In some cases, PropAMMs may show tight quotes to attract order flow and then widen their spreads before execution. Smart Settlement eliminates this by selecting the actual best pool at swap time.
* **Better Execution on Volatile or Meme Pairs** - Especially useful during high volatility when other traders front-run your swap and leave a price impact on an otherwise good pool at quote time. Smart Settlement will select the more liquid pool with a lower price impact
* **Seamless & Automatic** - No extra steps - just keep swapping on KyberSwap or any other integrating partners.
* **No Additional Protocol Fee** - Smart Settlement does not add any protocol fee. As per [Fee Schedule](../../../user-guide/fee-schedule.md), KyberSwap does not charge fees to users using the protocol to swap tokens.

## Supported Chains

Smart Settlement is currently available on: Ethereum, Base, Arbitrum, Avalanche, Berachain, Polygon.

It is rolling out gradually and will be expanded to more supported chains. Check [KyberSwap.com](https://kyberswap.com) for up-to-date availability.

## How It Works

1. You select input and output tokens + amount (just like a normal swap).
2. **Smart Settlement** automatically detects pools with high slippage risk (e.g. small pools, PropAMM pools...) and proposes extra candidate pools for on-chain comparison.
3. You click **Swap** and submit the transaction.
4. At execution time, KyberSwap's contract compares all candidate pools as proposed.
5. For each swap hop, it compares and picks the one pool that **maximizes the output tokens**.
6. The transaction executes with the best possible outcome.

This happens in the background - you simply enjoy a better result with stronger protection.

<table data-full-width="false"><thead><tr><th>Scenario</th><th>Previous Behaviour</th><th>Smart Settlement</th></tr></thead><tbody><tr><td>Routes through a hot Uniswap V2 pool and gets too high slippage</td><td>Transaction reverts</td><td>Checks both Uniswap V2 and Uniswap V3 and picks Uniswap V3 pool, transaction succeeds.</td></tr><tr><td>Routes through a PropAMM pool and gets lower amount than quoted</td><td>User receives less tokens than quoted</td><td>On-chain comparison selects the better pool; user receives more tokens compared to previous behaviour.</td></tr><tr><td>Swapping for a meme coin</td><td>Routes through pools selected at quote time and gets some slippage</td><td>Onchain comparison picks a pool that just got a big sell (and thus offers better price), user receives the expected amount with no slippage.</td></tr></tbody></table>

### Frequently Asked Questions

1. **How is Smart Settlement different from Dynamic Trade Routing?**\
   [Dynamic Trade Routing](dynamic-trade-routing.md) determines the optimal route across liquidity sources at quote time - before the transaction is submitted. Smart Settlement operates at execution time, comparing candidate pools on-chain at the moment the transaction is processed. The two mechanisms work in combination: Dynamic Trade Routing selects the route, Smart Settlement selects the best pool within that route at execution.
2. **Which tokens or pairs benefit most from Smart Settlement?**\
   Smart Settlement is most effective for low-liquidity tokens, newly launched tokens, and pairs with high price volatility. It is also particularly beneficial for large swap amounts where price impact across pools is more significant.
3. **Will Smart Settlement always find a better pool?**\
   Not necessarily. If the originally quoted pool remains the best option at execution time, Smart Settlement will route through it as normal. The on-chain comparison only changes the selected pool when a better alternative exists at the moment of execution.
4. **Can Smart Settlement cause my transaction to fail?**\
   No. Smart Settlement does not introduce additional revert conditions. If no better pool is found, execution proceeds through the originally quoted route. Your existing slippage tolerance setting remains the primary protection against transaction failure.
5. **Does Smart Settlement interact with KyberSwap Limit Orders?**\
   Yes, any swaps with slippage risk may use Smart Settlement. Moreover, KyberSwap Limit Orders can also be used as additional candidate pools given good price/liquidity
6. **Does Smart Settlement protect against PropAMM spoofing?**\
   Yes — by comparing pools on-chain at execution time, it prevents PropAMM operators from showing attractive quotes and then worsening them before your trade settles.
7. **Is Smart Settlement slower?**\
   No. The on-chain comparison is atomic and completes within the same transaction just like a normal swap.
8. **Does it cost more gas?**\
   Gas cost may be slightly higher in some cases due to the extra pool checks, but optimizations are in place to ensure minimal added gas cost. The feature is tuned so that the extra tokens you receive almost always outweigh the small gas difference. Smart Settlement will be more prominent on low-gas chains.
9. **Can I still set my own slippage tolerance?**\
   Yes - Smart Settlement works together with your chosen slippage setting for extra protection.

{% hint style="info" %}
Smart Settlement is currently available only to selected client IDs. Smart Settlement is rolling out gradually and will be expanded over time. If you are interested, reach out to us on #business-outreach channel on [Discord](https://discord.gg/kyberswap) or at [**business@kyber.network**](mailto:business@kyber.network).
{% endhint %}

## Need Help?

* Join our [Discord](https://discord.gg/kyberswap) or [Telegram](https://t.me/kyberswap) for support.
* Check the full [KyberSwap User Guide](/broken/pages/mxns8qL7odOMYPx9JS4K) for more trading tips.
* Developers: See the [Aggregator EVM API](../../aggregator-api/aggregator-api-specification/evm-swaps.md) for integrating KyberSwap with Smart Settlement into your dApp.

***

**Ready to maximize your returns?** Head to the [swap page](https://kyberswap.com/swap/ethereum) and try out Smart Settlement on your next trade.
