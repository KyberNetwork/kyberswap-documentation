---
description: All-in-one Liquidity Hub for Liquidity Providers
---

# Kyber Earn

## Introduction

### Overview

[Kyber Earn](https://kyberswap.com/earn) is an all-in-one platform that lets you discover, enter, and manage liquidity positions across multiple protocols — including Uniswap V3, Uniswap V4, PancakeSwap, Aerodrome, SushiSwap, etc. - from a single interface.

Instead of switching between DEXs to compare pools, manually balancing tokens, or tracking positions across different dashboards, Kyber Earn brings everything together. You can explore and compare earning opportunities with rich visual analytics, enter positions using any tokens you hold, and actively monitor and adjust your liquidity - all in one place.

{% hint style="info" %}
Kyber Earn does not operate liquidity pools directly. It provides tooling to interact with pools on third-party protocols, currently including Uniswap V3, Uniswap V4, PancakeSwap, Aerodrome, and SushiSwap, among others. For a comprehensive list of supported chains and protocols, refer to [Supported Exchanges And Networks](../../getting-started/supported-exchanges-and-networks.md).
{% endhint %}

### **Integrated Technologies: Zap technology**

All deposit, withdrawal, migration, repositioning, and compounding operations within Kyber Earn are powered by [Zap as a Service (ZaaS)](../../developer-guide/zap-as-a-service-zaas-api/). ZaaS automatically handles the token swaps and calculations needed to enter or exit a position, so you don't have to do it manually.

Key highlights:

* **Up to 5 input tokens** — Deposit into any pool using up to 5 different tokens in a single transaction, an industry-first for concentrated liquidity.
* **Optimized routing** — All swaps are routed through the [KyberSwap Aggregator](https://docs.kyberswap.com/kyberswap-solutions/kyberswap-aggregator), optimizing for the best rate, minimal price impact, and gas efficiency.
* **Fallback logic** — If the primary swap route encounters issues, KyberZap automatically simulates and executes alternative routes to maximize capital usage.

For full technical details, see the [**Zap as a Service (ZaaS) documentation**](../../developer-guide/zap-as-a-service-zaas-api/)**.**

## Key Benefits

### Discover & Compare Pools with Rich Insights

Kyber Earn aggregates pools across supported protocols and gives you the data you need to make informed decisions — not just a single APR number.

*   **Real-Time Metrics** - Browse pools with live data on APR (including Est. Pool APR, Active APR, Max APR), fees earned, TVL, volume, and rewards.

    <figure><img src="../../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure>
*   **Five APR Metrics** — Go beyond standard Est. pool APR. Kyber Earn surfaces five distinct APR metrics — Est. Pool APR, Active APR, Max APR, Est. Position APR, and Est. My Position APR — so you can evaluate pools and positions with precision. See the [APR Metrics page](https://docs.kyberswap.com/user-guide/kyber-earn/apr-metrics) for a full breakdown of how each is calculated and when to use it.

    <figure><img src="../../.gitbook/assets/image (191).png" alt=""><figcaption></figcaption></figure>
* **Pool Categories** — Pools are grouped into three categories to help you filter by strategy:
  * **Farming** — Pools with active reward programs, earning you additional token rewards on top of LP fees.
  * **Highlighted** — Pools matching tokens in your connected wallet, or top volume pools if no wallet is connected — a personalized starting point.
  * **Low Volatility** — Stablecoin and correlated-asset pools with steady yield and minimal impermanent loss risk.
  * **High APR** — Pools offering the highest aggregate yields, suited for LPs comfortable with higher price volatility.
  * **Solid Earning** — Pools with the highest trading fees over the past 7 days, indicating consistent, organic volume.

### Visualized Pool & Position Data

Every pool detail page is organized into three tabs — **Information**, **Earning(s)**, and **Analytics** — so performance is actually readable, not buried in raw numbers.

*   **Information** — View pool metrics at a glance: TVL, 24h volume, 24h fees, rewards, liquidity utilization, and an interactive APR history chart over 24h, 7d, or 30d. The chart overlays Est. Pool APR, Active APR, and volume so you can see how yields have trended over time.

    <figure><img src="../../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>
*   **Earning(s)** — See the earning history for any pool, broken down by source: LP Fees, LM (Liquidity Mining) Rewards, EG (Equilibrium Gain) Sharing, and Bonus (other incentives). A donut chart shows the total earned and how it splits across sources, while a bar chart tracks daily earnings over your selected period. APR and Active APR are displayed with their fee and reward components side by side.

    <figure><img src="../../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>
*   **Analytics** — Access pool price candlestick charts (24h, 7d, 30d) powered by [Token Settlement Price](../../developer-guide/start-here/foundational-solutions/token-settlement-price.md) - derived from real on-chain swap events - alongside a liquidity flows chart showing add/remove activity, net flow, and TVL over time.

    <figure><img src="../../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

### More Reward Opportunities

Kyber Earn surfaces multiple earning layers beyond standard trading fees:

* **FairFlow Rewards** — Pools running on Uniswap V4 or similar protocols with [KyberSwap FairFlow](../kyberswap-fairflow/) generate additional yield for LPs through two reward components:
  * **EG (Equilibrium Gain) Sharing** — Rewards from arbitrage value captured by the FairFlow swap hook, distributed to LPs.
  * **LM (Liquidity Mining) Rewards** — Token incentives allocated to LPs participating in FairFlow pools.
* **Bonus Rewards via Merkl** — Additional bonus incentives sourced through Merkl are displayed directly in the pool detail view, so you can see the full earning potential of a pool before entering.

### Enter Any Pool in One Transaction

Entering a concentrated liquidity position normally requires multiple steps: swapping tokens in separate transactions to match the pool's required ratio, calculating exact amounts, and then depositing. Kyber Earn removes this friction with [**our Zap technology**](../../developer-guide/zap-as-a-service-zaas-api/).

* **Flexible Entry** — Supply liquidity using any combination of up to 5 tokens from your wallet. KyberSwap’s Zap handles all the swapping and ratio balancing for you.
* **Instant Migration** — Use Zap Migrate to move capital from an existing position to a new pool in a single atomic transaction — no need to withdraw, swap, and redeposit manually.

#### Track & Manage Your Positions

Once you've entered positions, Kyber Earn gives you a unified dashboard to monitor performance and manage your liquidity — all from one place.

* **Unified Dashboard** — Track accrued fees, rewards, and position status (in-range vs. out-of-range) across all your positions, chains, and protocols.
* **Full Position Management** — Increase liquidity, claim fees, withdraw (partially or fully), set up or view your active Smart Exit orders — every action you need to manage a position is accessible from the dashboard.
* **One-Click Repositioning** — When the market moves and your position goes out of range, reposition to a new price range in a single transaction. Kyber Earn automatically withdraws, claims fees, rebalances, and redeposits for you — no manual steps required.
* **Smart Exit** — Set predefined exit conditions (e.g., "exit if ETH drops below $2,000") and Kyber Earn will automatically withdraw your position when those conditions are met — no need to monitor 24/7. See the [Smart Exit documentation](../smart-exit/) for full details.

## Core Capabilities

[Kyber Earn](https://kyberswap.com/earn) provides a unified interface for interacting with supported liquidity pools and managing yield-generating positions. The following core capabilities are available to users:

#### **Position Creation**

* **Zap In (Single or Multi-Token)** — Enter any pool using 1 to 5 tokens of your choice. The tokens don't need to match the pool's pair — KyberZap swaps them into the correct ratio via the [KyberSwap Aggregator](../../developer-guide/aggregator-api/) with minimal price impact.
* **Zap Migrate** — Move capital from an existing position directly into a new pool in one transaction. Your current position is exited, fees are claimed, and assets are swapped and redeposited into the target pool automatically.

#### **Position Management, Increase Liquidity and Reposition**

You can view and manage all your existing positions from the [My Positions](https://kyberswap.com/earn/positions) dashboard.

* **Performance Tracking** — Monitor accrued trading fees, [FairFlow](https://docs.kyberswap.com/kyberswap-solutions/kyberswap-fairflow) rewards, bonus rewards, and whether each position is in-range or out-of-range — all in real time.
* **Increase Liquidity** — Increase the size of an existing position by zapping in additional assets. The protocol automatically calculates the exact token ratio required by your specific price range and handles the underlying conversions for you, with the same execution flow as a standard Zap In.
* **Repositioning** — Adjust your position to a new price range when the market shifts. Kyber Earn withdraws your liquidity, claims accrued fees, rebalances the assets for the new range, and redeposits — all in one transaction.

#### **Fee and Reward Management**

Users can view and manage fees and rewards generated by their liquidity positions directly within Kyber Earn.

* **Claiming** — Accrued trading fees can be claimed per position at any time from the My Positions dashboard.
  * FairFlow rewards are separate from trading fees and governed by a vesting schedule. The accumulated reward amount becomes claimable after the vesting period concludes at the end of each FairFlow cycle. Refer to the [FairFlow documentation](../kyberswap-fairflow/) and information on the interface for cycle timing and claim details.
* **One-Click Compounding** — Automatically reinvest accrued fees for each position back into the core principal of the corresponding position in one transaction, maximizing the effects of compound interest without manual asset swapping.

#### **Advanced Exit Strategies**

Users have flexible options to withdraw their capital, tailored to specific market conditions and risk parameters:

* **Zap Out (Single Asset)** — Withdraw partially or fully remove a position, then automatically swap the underlying pool assets into a single target token of your choice. This operation is powered by KyberZap, which routes the consolidation swap through the KyberSwap Aggregator to minimize price impact.
* **Standard Withdrawal** — Withdraw partially or fully remove a position manually, receiving the underlying pool assets in their current ratio, no additional swaps. Accrued fees are collected in the same transaction.
* [**Smart Exit**](../smart-exit/) (Industry-First Intent-Based Liquidity Withdrawal) — Leverage a unique, intent-based market solution to conditionally remove liquidity. Rather than monitoring active ticks 24/7, users simply define specific exit conditions. Liquidity is withdrawn only when these specific conditions are triggered, ensuring execution is strictly enforced and fully verifiable via public smart contracts.
  * **Example scenario:** An LP holds a ETH/USDC position with a price range of $2,200–$2,800. They submit a Smart Exit condition to trigger if the ETH price drops below $2,100 or after 12:00, April 1, 2026. If the on-chain ETH price is ≤ $2,100, the Smart Exit contract withdraws the position and returns the pool assets to the LP’s wallet, limiting further impermanent loss exposure below that level. If the price condition is never met, the position is automatically withdrawn at or after 12:00 on April 1, 2026.
  * Notes:
    *   Submitting, cancelling, and modifying Smart Exit conditions are handled off-chain - no gas is required for these actions. The only on-chain transaction occurs when exit conditions are triggered and the position withdrawal is executed.

        * Smart Exit returns assets in the pool token ratio. It does not consolidate into a single token - an automatic Zap Out as part of the Smart Exit flow is not currently supported.

        For comprehensive technical details and guidelines, you can refer to: [Smart Exit documentation](../smart-exit/).

{% hint style="warning" %}
Before confirming any Zap operation (Zap In, Zap Out, Migrate, or Reposition), always review the quoted output, slippage, Zap impact, and applicable fees displayed in the interface.
{% endhint %}

#### **Permissionless Pool Creation**

* **Custom Pool Creation** — If a desired pair and fee tier do not exist, users can initialize a new liquidity pool directly through the Kyber Earn interface using any combination of up to 5 tokens, setting the foundational liquidity parameters for the market.

{% hint style="info" %}
Disclaimer: KyberSwap provides tools for tracking and managing liquidity on third-party protocols. KyberSwap does not operate, control, or guarantee the performance of any third-party pool. Any pool-related concerns should be directed to the corresponding protocol.
{% endhint %}

### Platform fee

All operations executed through [the KyberZap contract](../../developer-guide/zap-as-a-service-zaas-api/contracts-and-addresses.md) incur a platform fee. The fee is charged on the input amount and varies based on the specific token pair category. The applicable fee amount is transparently displayed in the interface for review prior to transaction confirmation.

Refer to [Fee Structure](../fee-schedule.md) for further details.



**Ready to start earning?** [Explore pools on Kyber Earn](https://kyberswap.com/earn) and manage all your LP positions — with deeper insights, visual analytics, and smarter tools — from one place.
