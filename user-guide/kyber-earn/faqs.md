---
description: Your Kyber Earn Questions Answered
---

# FAQs

## General

<details open>

<summary>How is Kyber Earn different from protocols like Uniswap, PancakeSwap, or Aerodrome?</summary>

Uniswap, PancakeSwap, and Aerodrome are liquidity protocols - they operate the pools. Kyber Earn is a management layer on top of these protocols, aggregating their pools into a single interface so LPs can discover, enter, and manage positions across multiple DEXs without switching between platforms.

Beyond aggregation, Kyber Earn adds capabilities not available natively on any single protocol: single/multi-token zapping (up to 5 tokens in one transaction), position migration, repositioning, fee compounding, zapping out into a single token, intent-based conditional exit via Smart Exit, five distinct APR metrics for smarter pool evaluation, and visual analytics including APR history, earning breakdowns by source, and pool price charts.

Kyber Earn does not replace these protocols — it enhances the experience of using them.

</details>

<details open>

<summary>How is Kyber Earn different from other liquidity management platforms?</summary>

Kyber Earn differentiates itself through Zap technology and deeper analytics. While most platforms only allow basic deposits matched to a pool's token pair, Kyber Earn enables LPs to supply liquidity using any combination of up to five tokens, regardless of the target pool's underlying pair. The platform automatically calculates ratios and routes conversions to minimize price impact.

Additionally, Kyber Earn provides five APR metrics (including Active APR for concentrated liquidity), visual earning breakdowns by source, pool price charts powered by on-chain settlement data, and industry-first innovations like Smart Exit for intent-based conditional liquidity withdrawal and Zap Migrate for single-transaction capital migration between pools.

</details>

<details open>

<summary>Is Kyber Earn safe to use?</summary>

Kyber Earn is an interface layer that aggregates pools from third-party protocols - it does not operate any pools directly. Any inherent risk associated with a specific pool belongs to that third-party protocol. Users are advised to independently assess the security of any protocol or pool before adding liquidity.

</details>

<details open>

<summary>What is impermanent loss, and how does Kyber Earn help?</summary>

Impermanent loss occurs when the price ratio of a pool's token pair changes from when you deposited, causing your position to be worth less than simply holding the tokens. Kyber Earn helps manage this through active range monitoring on the dashboard (showing in-range vs. out-of-range status in real time), one-click repositioning (realigning to a new range without manual steps), and Smart Exit (automatically withdrawing when a price threshold, fee target, or time limit is triggered - limiting further exposure).

</details>

<details open>

<summary>What are the different APR metrics on Kyber Earn?</summary>

Kyber Earn displays five APR metrics to help you evaluate pools and positions at different levels of detail:

* **Est. Pool APR** — Annualized return based on total fees earned by the pool over the selected time window (24h, 7d, or 30d), relative to total pool TVL. Serves as the standard baseline metric for comparing pool performance.
* **Active APR** — Annualized return based on earnings relative to active TVL only - liquidity currently within the price range. Excludes out-of-range capital from the denominator.
* **Max APR** — The highest APR observed across all positions in the pool. Represents the return ceiling for a strategically placed position.
* **Est. Position APR** — Estimated annualized return for a new position at a selected price range. Based on projected fee earnings and applicable rewards under current conditions. Provided for reference only and does not guarantee future returns.
* **Est. My Position APR** — Annualized return of an existing position, calculated from fees earned relative to its current value over the selected time window. Reflects realized performance.

Most platforms only show a single pool APR. These five metrics let you compare pools more accurately and understand how your specific range and capital affect your real yield. For a full breakdown of how each is calculated, see the [APR Metrics page](apr-metrics.md).

</details>

<details open>

<summary>What rewards can I earn on Kyber Earn besides trading fees?</summary>

Beyond standard LP trading fees, Kyber Earn surfaces additional reward layers depending on the pool:

* [**FairFlow Rewards**](../kyberswap-fairflow/) — Pools running on Uniswap V4, PancakeSwap V4, etc. with KyberSwap FairFlow generate two additional reward components: EG (Equilibrium Gain) Sharing from captured arbitrage value, and LM (Liquidity Mining) Rewards as token incentives following a vesting schedule per cycle.
* **Bonus Rewards via Merkl** — Select pools offer additional bonus incentives sourced through Merkl, displayed directly in the pool detail view.

You can see the full earning breakdown — LP Fees, LM Rewards, EG Sharing, and Bonus — in the Earning(s) tab on any pool detail page. Use the Farming pool category to quickly filter for pools with active reward programs.

</details>

## How-To and Operations

<details open>

<summary>How do I find the best pool for my risk profile on Kyber Earn?</summary>

Kyber Earn segments pools into three categories - Low Volatility, High APR, and Solid Earn - to match different LP strategies. Use Low Volatility for stablecoin or correlated pairs with minimal impermanent loss risk. Use High APR for maximum yield potential with higher price volatility. Use Solid Earn for pools with proven, consistent trading volume.

</details>

<details open>

<summary>How do I move liquidity from one pool to another?</summary>

Use Zap Migrate when you select the liquidity source when adding a new position. It exits your existing position and deploys the withdrawn assets into a new target pool atomically in a single transaction, without requiring you to manually withdraw, swap, and redeposit.

</details>

<details open>

<summary>What is the best way to protect my liquidity position from market movement?</summary>

Users can utilize the [Smart Exit](../smart-exit/) feature for a position to establish automated withdrawal parameters. Smart Exit supports 3 types of exit conditions: pool price thresholds, target fee yields, and specific time limits. By configuring these parameters, the smart contract will automatically execute the liquidity withdrawal when the defined conditions are met. This allows users to manage exposure to price volatility, withdraw based on yield performance, or remove liquidity after a set duration without requiring manual intervention.

</details>

<details open>

<summary>Can I provide liquidity with just one token?</summary>

Users can add liquidity using a single token via the Zap In feature. The protocol utilizes the KyberSwap Aggregator to automatically calculate and execute the necessary underlying token swaps to match the target pool's required reserve ratio. Additionally, users can choose to fund a position using any custom combination of up to 5 distinct tokens.

</details>

<details open>

<summary>How do I compound my liquidity position earnings?</summary>

Choose a position you want to compound and open the pool details. Navigate to the "Unclaimed fee" section, select Claim, and then click Compound. It collects your accrued trading fees and reinvests them back into your position in a single transaction, increasing your position size without manual swapping.

</details>

<details open>

<summary>What should I do when my position goes out of range?</summary>

You have three options: wait for the price to return to your range; use Repositioning to move your liquidity to a new range aligned with the current price; or withdraw using Standard Withdrawal or Zap Out if you want to exit entirely or partially.

</details>

<details open>

<summary>Why is my position APR less than the pool APR shown?</summary>

There are two common reasons:

* **Wide price range:** A wider range spreads your liquidity across more ticks, reducing your share of active liquidity and therefore your share of fees earned relative to your position value. Consider using Reposition to adjust to a narrower range around the current price.
* **High competition:** As more LPs deposit into the same pool, the total TVL increases. If fee earnings do not grow proportionally, the APR is diluted across a larger capital base. Consider increasing your liquidity to maintain your share of fees.

For a detailed explanation of how each APR metric is calculated — including Est. Position APR and Est. My Position APR which reflect your specific range and capital — see the [APR Metrics page](apr-metrics.md).

</details>
