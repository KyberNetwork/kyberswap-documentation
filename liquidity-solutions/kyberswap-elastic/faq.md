---
description: Your KyberSwap Elastic Questions Answered
---

# FAQ

## General

<details>

<summary>What is KyberSwap Elastic?</summary>

KyberSwap Elastic is an improved version of our revolutionary Decentralized Market Maker platform (now known as “KyberSwap Classic”) that lets Liquidity Providers maximize capital efficiency by enabling liquidity concentrations across multiple customizable price ranges. This results in better slippage, transaction volume, and earnings for Liquidity Providers.

For more information on KyberSwap Elastic, please refer to the [KyberSwap Elastic Docs](./) or [this blog post](https://blog.kyber.network/announcing-our-new-kyberswap-protocol-kyberswap-elastic-9cab14259d4a) on KyberSwap Elastic.

</details>

<details>

<summary>What is the difference between Classic vs Elastic?</summary>

Both KyberSwap Classic and Elastic are [AMM](../../getting-started/foundational-topics/decentralized-finance/automated-market-maker.md) liquidity solutions that were created with the intent of optimizing LP yields through greater capital efficiency. KyberSwap Classic enables pools to be configured with [dynamic fees](../kyberswap-classic/concepts/flexible-fee-adjustment.md) which respond to market conditions while KyberSwap Elastic enables users to enter into [concentrated liquidity](concepts/concentrated-liquidity.md) positions with [auto-compounding fees](concepts/reinvestment-curve.md).

For the full comparison, please refer to [Classic vs Elastic](../classic-vs-elastic/).

</details>

<details>

<summary>Which chains does KyberSwap Elastic Support?</summary>

The full list of supported chains can be found on [Supported Exchanges and Networks](../../getting-started/supported-exchanges-and-networks.md).

</details>

<details>

<summary>Which tokens does KyberSwap Elastic support?</summary>

KyberSwap whitelists well-known tokens for ease of access, but you can import custom tokens that meet the ERC20 standard via our user interface. For more information on how to do this, please refer to [Add Your Favourite Tokens](../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md).

</details>

<details>

<summary>Is KyberSwap Elastic a fork of Uniswap V3?</summary>

## KyberSwap Elastic is NOT a fork of Uniswap V3

Uniswap V3 source code is under [Business Source License 1.1](https://github.com/Uniswap/uniswap-v3-core/blob/main/LICENSE) meaning it is **not fully open source**. This agreement incorporates copyright law and allows Uniswap governance to restrict unauthorized commercialization of its source code until 2023.

KyberSwap Elastic was developed with **our own proprietary code**. It is only similar to Uniswap V3 in the sense that both are [tick-based](concepts/tick-range-mechanism.md) AMMs with [customizable price ranges](concepts/concentrated-liquidity.md), and use NFTs to represent liquidity positions, but that’s where the similarities end.

KyberSwap Elastic’s protocol maintains more than 1 AMM curve at the same time, in the same smart contract. In Elastic, we have two curves: The Investment Curve where liquidity positions are tracked and the [Reinvestment Curve](concepts/reinvestment-curve.md) where yields are auto-compounded over an infinite price range. This design enables Elastic LPs to earn more yield as fees are automatically compounded and do not sit idly waiting to be collected.

Another key difference is in our [Anti JIT / Snipe protection](concepts/anti-sniping-mechanism.md), which is something Uniswap V3 currently does not offer. KyberSwap Elastic protects our Liquidity Providers’ earnings by implementing a very short locking / vesting period (1–2 blocks).

Additionally, KyberSwap Elastic also offers [additional fee tiers](user-guides/elastic-pool-creation.md#fee-tier-options) which allow LPs to have more fine-grained control over their risk-adjusted returns.

### Further Reading

For more information on this topic, please refer to [this blog post](https://blog.kyber.network/kyberswap-elastic-vs-uniswap-v3-a-comparison-7e115117d795).

For more information about the differences between KyberSwap Elastic and Uniswap V3, please refer to [this article](https://support.kyberswap.com/hc/en-us/articles/13766696328729).

</details>

## Liquidity provision

<details>

<summary>How wide/narrow should I set my price range?</summary>

KyberSwap Elastic pools allow you to [specify liquidity concentration ranges](user-guides/elastic-pool-creation.md#step-4-set-price-range). When the market price of the asset pair is within this specified price range, price takers can trade using the liquidity you have deposited to the pool. You can make the range as wide or as narrow as you want but there are some tradeoffs to consider in each case.

#### Wide Range

When the range is set to be relatively wide, the pool has a lower chance of going out of range so it will remain in operation for more time, but you will earn less fees on each transaction since your liquidity is spread out more thinly across a wider range.

#### Narrow Range

When the range is set to be relatively narrow, your liquidity is more concentrated which will result in higher fees earned per transaction, but this comes at the higher risk of the pool going out of range resulting in longer periods when your liquidity is not being traded against.

KyberSwap also provides a list of preset options for your convenience which can be viewed [here](user-guides/elastic-pool-creation.md#step-4-set-price-range).

</details>

<details>

<summary>What fee tier should I set?</summary>

There are ten tiers of fees you can set on your liquidity concentration ranges in KyberSwap Elastic. These options correspond to the relative price correlation between token pairs and the full list can be found [here](user-guides/elastic-pool-creation.md#fee-tier-options).

</details>

## Elastic farming

<details>

<summary>What is a yield farm</summary>

A Yield Farm (also known as a Liquidity Mining Pool or “Farming Pool” on KyberSwap) is a type of DeFi protocol that allows Liquidity Providers (LPs) to passively earn a return on capital contributed to a liquidity pool. The Yield Farm provides LPs with rewards over time to incentivize LPs to continue to provide liquidity to the pool as well as to help offset the risk of [Impermanent Loss](../../getting-started/foundational-topics/decentralized-finance/impermanent-loss.md).

</details>

<details>

<summary>How do I tell what rewards a Farming pool offers?</summary>

To incentivize yield farming on our platform, we usually offer KNC token as a reward for staking activity in our active farming pools. From time to time we also jointly offer other tokens with our partners as staking rewards. You can easily tell which active farming pools offer KNC or KNC and another token when you look at the pool details in list view. Select the list view icon on the Active farms page to toggle this view.

<img src="https://support.kyberswap.com/hc/article_attachments/14216593542425" alt="001_FarmsListView.png" data-size="original">

From here you can see the types of coins offered under the “My Rewards” column. For example, in the following graphic, the first three farms offer both KNC and LDO as rewards, whereas the following three farms on the list offer just KNC.

<img src="https://support.kyberswap.com/hc/article_attachments/14216593573017" alt="002_MyRewardsColumn.png" data-size="original">

</details>

<details>

<summary>What are the different farm types on KyberSwap Elastic?</summary>

Elastic farms supports multiple farming mechanisms which can be based on time-based liquidity, target volume, or operator defined farm ranges. Please refer to [Tick-Based Farming](concepts/tick-based-farming.md) for a more detailed explanation of the various mechanisms.

</details>

<details>

<summary>How are farming rewards calculated on KyberSwap Elastic?</summary>

Rewards are distributed based on 2 mechanisms: active time and target volumes. You can refer to [Tick-Based Farming](concepts/tick-based-farming.md) for the exact details on how farm types are determined.

</details>

<details>

<summary>How do I tell if an Elastic Farm is Type 1 or Type 2?</summary>

KyberSwap Elastic supports 2 types of farms based on the active time and target volumes mechanism detailed in [Tick-Based Farming](concepts/tick-based-farming.md). You can tell at a glance which of the two any given pool uses. Simply refer to the “My Deposit | Target Volume” column on the Active Pools page.

<img src="https://support.kyberswap.com/hc/article_attachments/14229147059353" alt="000_FarmingMechs.png" data-size="original">

In the above graphic, the first farm is a Type 2 farm since it has a target volume. Type 2 farms will also show progress bars for the target volume achieved to date. In contrast, the second farm is a Type 1 farm that does not have any target volume associated with it, only a deposit value.

</details>

<details>

<summary>Is there a deadline for collecting my Yield Farming rewards?</summary>

There is no deadline for collecting (aka harvesting) your pool farm rewards. However please note that some farming pools have vesting periods: after harvesting, the rewards can only be withdrawn after a set vesting period. The vesting period counter starts at the point of collection.

Please refer to [Harvesting and claiming rewards](broken-reference) for further details.

</details>

<details>

<summary>How long is the vesting period for yield farming rewards?</summary>

Farming pool rewards can be withdrawn after they vest. The vesting period varies from pool to pool, with some farming pools not having a vesting period. You can check the vesting period of the farm you’re participating in by navigating to the Vesting tab on the Farms page. Note that the vesting period counter starts at the point of collection.

</details>

## Troubleshooting

<details>

<summary>My Elastic Pool APR looks wrong</summary>

We sometimes get questions from users who notice a discrepancy between the APR estimates for their positions and the APR estimates for the KyberSwap Elastic pool as a whole. For example, in the following case, the AVAX-USDC (Avalanche) Elastic Pool total Average APR (322.04%) seems to dwarf the user’s position’s total APR (137.62%).

<img src="https://support.kyberswap.com/hc/article_attachments/14459979237017" alt="001b_PoolAPR.png" data-size="original">

<img src="https://support.kyberswap.com/hc/article_attachments/14460000295193" alt="001a_PositionAPR.png" data-size="original">

This is because the pool APR estimate (i.e. the APR due to LP fees) for the entire pool is calculated based on the average of all the in-range positions in the pool. Some positions may have price ranges that are set to be very aggressive, so their APRs seem high, but that assumes an ideal world where the position never goes out of range. In reality, positions with overly-aggressive narrow price ranges run the risk of the quickly going out of range and becoming inefficient.

The pool APR estimate shown specific to your position takes the price range that you set into account, so while it does seem much lower than the pool's total average APR estimate, it is also likely to be more in line with reality as your position is likely to remain in range for longer.

Please refer to [Elastic APR Calculations](concepts/apr-calculations.md) for the exact logic and formula behind the various APR calculations.

</details>

<details>

<summary>I cannot unstake from the SIPHER - wETH farming pool</summary>

We sometimes receive questions from users who are unable to unstake positions from the SIPER-wETH KyberSwap Elastic Farm on the Ethereum network. The transaction fails due to an error message that resembles the following:

```
cannot estimate gas; transaction may fail or may require manual gas limit
```

This is likely due to the unique nature of the SIPHER-wETH farming pool. This pool works slightly differently from the usual KyberSwap Elastic farming pools.

In order to generate rewards, in addition to staking your liquidity position on KyberSwap, you would also have had to stake Kyber SLP tokens on the [Sipher portal](https://sipher.xyz/stake/deposit/kyber-slp-sipher-eth). It follows therefore that in order to unstake the position on KyberSwap, you will first need to unstake and withdraw your Kyber SLP tokens from the Sipher portal before you will be allowed to unstake and withdraw the position on KyberSwap.

For more information on this pool, please refer to [this blogpost](https://blog.kyber.network/sipher-partners-with-kyberswap-on-50-million-liquidity-mining-campaign-to-provide-the-best-1cb5b9d6f44).&#x20;

</details>

Still can't find what you're looking for? Check out the [KyberSwap Help Center](https://support.kyberswap.com/hc/en-us).
