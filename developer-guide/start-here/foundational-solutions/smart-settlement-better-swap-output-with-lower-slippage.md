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
* **Better Execution on Volatile or Meme Pairs** - Especially useful during high volatility when other traders front-run your swap and leave a price impact on an otherwise good pool at quote time. Smart Settlement will select the more liquid pool with a lower price impact.
* **Resilience Against MEV and Sandwich Attacks** - Even when the originally selected pool is sandwiched or front-run within the same block, Smart Settlement can detect the worsened rate and switch to a better pool. This provides an additional layer of resilience on top of your existing slippage protection.
* **Protection Against JIT Liquidity Removal** - In some cases, liquidity providers may add liquidity to a pool temporarily — to appear deep and attractive to aggregators, or to farm trading fee rewards and liquidity mining incentives — then remove it before execution. When this happens, the pool is shallower than expected and delivers worse output. Smart Settlement detects this on-chain at execution time: if the pool’s liquidity has been pulled and output has worsened, it switches to a pool with sufficient depth instead.
* **Seamless & Automatic** - No extra steps - just keep swapping on KyberSwap or any other integrating partners.
* **No Additional Protocol Fee** - Smart Settlement does not add any protocol fee. As per [Fee Schedule](../../../getting-started/fee-schedule.md), KyberSwap does not charge fees to users using the protocol to swap tokens.

## Supported Chains

Smart Settlement is available on all chains supported by the KyberSwap Aggregator. For the list of supported chains, refer to [Supported Exchanges and Networks](../../../getting-started/supported-exchanges-and-networks.md).

## How It Works

<figure><img src="../../../.gitbook/assets/smart settlement.png" alt=""><figcaption></figcaption></figure>

1. You select input and output tokens + amount (just like a normal swap).
2. **Smart Settlement** automatically detects pools with high slippage risk (e.g. small pools, PropAMM pools...) and proposes extra candidate pools for on-chain comparison.
3. You click **Swap** and submit the transaction.
4. At execution time, KyberSwap's contract compares all candidate pools as proposed.
5. For each swap hop, it compares and picks the one pool that **maximizes the output tokens**.
6. The transaction executes with the best possible outcome.

This happens in the background - you simply enjoy a better result with stronger protection.

<table data-full-width="false"><thead><tr><th>Scenario</th><th>Previous Behaviour</th><th>Smart Settlement</th></tr></thead><tbody><tr><td>Routes through a hot Uniswap V2 pool and gets too high slippage</td><td>Transaction reverts</td><td>Checks both Uniswap V2 and Uniswap V3 and picks Uniswap V3 pool, transaction succeeds.</td></tr><tr><td>Routes through a PropAMM pool and gets lower amount than quoted</td><td>User receives less tokens than quoted</td><td>On-chain comparison selects the better pool; user receives more tokens compared to previous behaviour.</td></tr><tr><td>Swapping for a meme coin</td><td>Routes through pools selected at quote time and gets some slippage</td><td>Onchain comparison picks a pool that just got a big sell (and thus offers better price), user receives the expected amount with no slippage.</td></tr></tbody></table>

### Frequently Asked Questions

**How is Smart Settlement different from Dynamic Trade Routing?**

[Dynamic Trade Routing](dynamic-trade-routing.md) determines the optimal route across liquidity sources at quote time - before the transaction is submitted. Smart Settlement operates at execution time, comparing candidate pools on-chain at the moment the transaction is processed. The two mechanisms work in combination: Dynamic Trade Routing selects the route and pool split, Smart Settlement verifies and can adjust the pool selection within that route at execution.

<table><thead><tr><th width="189.91796875"></th><th>Before: Dynamic Trade Routing only</th><th>After: Dynamic Trade Routing + Smart Settlement</th></tr></thead><tbody><tr><td>When the pool is selected</td><td>At quote time — before you submit the transaction</td><td>At execution time — on-chain, inside your transaction</td></tr><tr><td>What it optimizes</td><td>Finds the best route and pool split across all available liquidity sources</td><td>Verifies the pool selection at the moment your swap executes, and switches to a better candidate pool if one is available.</td></tr><tr><td>What happens if pool conditions change during execution time</td><td>You may receive whatever rate the pool offers at execution, even if it has worsened since quoting, as long as it remains above your minimum accepted return amount.</td><td>Smart Settlement detects the worsened rate and can switch to a better candidate pool at execution time, potentially improving your final output.</td></tr><tr><td>PropAMM shows a tight quote then widens spread</td><td>You may receive fewer tokens than quoted</td><td>Smart Settlement detects the worse rate on-chain and switches to a pool with better output</td></tr><tr><td>Your pool gets sandwich-attacked</td><td>You may absorb the price impact and receive fewer tokens than quoted.</td><td>Smart Settlement detects the impact and can switch to an unaffected pool with better output.</td></tr><tr><td>Liquidity is removed after quoting</td><td>You may experience higher slippage due to shallower pool depth and receive fewer tokens than quoted.</td><td>Smart Settlement detects the reduced depth and can switch to a pool with sufficient liquidity.</td></tr><tr><td>Transaction revert risk</td><td>Swap reverts if slippage exceeds your tolerance</td><td>Fallback candidates reduce revert rate — if the main pool would revert, an alternative can execute instead</td></tr><tr><td>Gas cost</td><td>Standard</td><td>Slightly higher in some cases due to on-chain pool comparisons. In most cases, the additional tokens received outweigh the small increase in gas cost.</td></tr><tr><td>User action required</td><td>None — automatic</td><td>None — automatic</td></tr></tbody></table>

**Which tokens or pairs benefit from Smart Settlement?**

Smart Settlement is most effective for low-liquidity tokens, newly launched tokens, and pairs with high price volatility. It is also particularly beneficial for large swap amounts where price impact across pools is more significant, and for pairs where the primary liquidity source is a PropAMM or PMM pool.



**Will Smart Settlement always find a better pool?**

If the originally quoted pool remains the best option at execution time, Smart Settlement will route through it as normal. The on-chain comparison only changes the selected pool when a better alternative exists at the moment of execution.



**Can Smart Settlement cause my transaction to fail?**

Smart Settlement does not introduce additional revert conditions. If no better pool is found, execution proceeds through the originally quoted route. In addition, Smart Settlement includes fallback mechanisms that can reduce the chance of transaction failure — if the main pool would revert, an alternative candidate pool may execute instead. Your existing slippage tolerance setting remains the primary protection against transaction failure.



**Does Smart Settlement interact with KyberSwap Limit Orders?**

Yes, any swaps with slippage risk may use Smart Settlement. Moreover, KyberSwap Limit Orders can serve as candidate pools when they offer competitive pricing and sufficient liquidity.



**Does Smart Settlement protect against PropAMM spoofing?**

Yes — by comparing pools on-chain at execution time, Smart Settlement can detect when a PropAMM operator has worsened their quoted rate before settlement, and switch to a pool with better output.



**Is Smart Settlement slower?**

No. The on-chain comparison is atomic and completes within the same transaction, just like a normal swap.



**Why does it cost more gas?**

Gas cost may be slightly higher in some cases due to the additional on-chain pool comparisons. Optimizations are in place to ensure minimal added gas cost. The feature is designed so that in most cases, the additional tokens you receive outweigh the small increase in gas cost. The cost-benefit ratio is strongest on low-gas chains where the gas overhead is negligible.



**Can I still set my own slippage tolerance?**

Yes. Smart Settlement does not change your existing trading experience or slippage settings on the interface. You can continue using your preferred slippage tolerance as usual.



**Why do I see "Call Failed" warnings on my transaction hash link?**

This is expected and your transaction has completed successfully. Smart Settlement works by trying multiple candidate pools on-chain within the same transaction. The candidates that are not selected will show as failed internal calls on the block explorer - because the contract checked them, found they weren't the best option, and moved on. These show as "Call Failed" on block explorers. The candidate that delivered the highest output is the one that actually executed your swap. Your transaction status and final token output are unaffected - in fact, these "Call Failed" entries are evidence that Smart Settlement actively compared pools to get you a better result.



{% hint style="info" %}
Smart Settlement is currently available only to selected client IDs. Smart Settlement is rolling out gradually and will be expanded over time. If you are interested, reach out to us on #business-outreach channel on [Discord](https://discord.gg/kyberswap) or at [**business@kyber.network**](mailto:business@kyber.network).
{% endhint %}

## Need Help?

* Join our [Discord](https://discord.gg/kyberswap) or [Telegram](https://t.me/kyberswap) for support.
* Check the full [KyberSwap User Guide](/broken/pages/mxns8qL7odOMYPx9JS4K) for more trading tips.
* Developers: See the [Aggregator EVM API](../../aggregator-api/aggregator-api-specification/evm-swaps.md) for integrating KyberSwap with Smart Settlement into your dApp.

***

**Ready to maximize your returns?** Head to the [swap page](https://kyberswap.com/swap/ethereum) and try out Smart Settlement on your next trade.
