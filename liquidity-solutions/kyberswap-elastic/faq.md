---
description: Your KyberSwap Elastic Questions Answered
---

# FAQ

<details>

<summary>Which chains does KyberSwap Elastic Support?</summary>

The full list of supported chains can be found on [Supported Exchanges and Networks](../../getting-started/supported-exchanges-and-networks.md).

</details>

<details>

<summary>Which tokens does KyberSwap Elastic support?</summary>

KyberSwap whitelists well-known tokens for ease of access, but you can import custom tokens that meet the ERC20 standard via our user interface. For more information on how to do this, please refer to [Add Your Favourite Tokens](../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md).

</details>

<details>

<summary>What is the difference between Classic vs Elastic?</summary>



</details>

<details>

<summary>Is KyberSwap Elastic a fork of Uniswap V3?</summary>

## KyberSwap Elastic is NOT a fork of Uniswap V3

Uniswap V3 source code is under [Business Source License 1.1](https://github.com/Uniswap/uniswap-v3-core/blob/main/LICENSE) meaning it is **not fully open source**. This agreement incorporates copyright law and allows Uniswap governance to restrict unauthorized commercialization of its source code until 2023.

KyberSwap Elastic was developed with **our own proprietary code**. It is only similar to Uniswap V3 in the sense that both are tick-based AMMs with customizable price ranges, and use NFTs to represent liquidity positions, but that’s where the similarities end.

KyberSwap Elastic’s protocol maintains more than 1 AMM curve as the same time, in the same smart contract. In Elastic, we have two curves: The Investment Curve and the Re-investment Curve. However, the protocol allows control over multiple curves.

It is this key difference in our technology that enables Elastic’s Fee **Compoundability**, which allows liquidity providers to earn more.

Another key difference is in our **Anti JIT / Snipe protection**, which is something Uniswap V3 currently does not offer. KyberSwap Elastic protects our Liquidity Providers’ earnings by implementing a very short locking / vesting period (1–2 blocks).

### Further Reading

For more information on this topic, please refer to [this blog post](https://blog.kyber.network/kyberswap-elastic-vs-uniswap-v3-a-comparison-7e115117d795).

For more information about the differences between KyberSwap Elastic and Uniswap V3, please refer to [this article](https://support.kyberswap.com/hc/en-us/articles/13766696328729).

</details>

<details>

<summary>How wide/narrow should I set my price range?</summary>

KyberSwap Elastic pools allow you to specify liquidity concentration ranges. When the market price of the asset pair is within this specified price range, price takers can trade using the liquidity you have deposited to the pool. You can make the range as wide or as narrow as you want but there are some tradeoffs to consider in each case.

### Wide Range

When the range is set to be relatively wide, the pool has a lower chance of going out of range so it will remain in operation for more time, but you will earn less fees on each transaction since your liquidity is spread out more thinly across a wider range.

### Narrow Range

When the range is set to be relatively narrow, your liquidity is more concentrated which will result in higher fees earned per transaction, but this comes at the higher risk of the pool going out of range resulting in longer periods when your liquidity is not being traded against.

KyberSwap also provides a list of preset options for your convenience which can be viewed [here](user-guides/elastic-pool-creation.md#step-4-set-price-range).

</details>

<details>

<summary>What fee tier should I set?</summary>

There are five tiers of fees you can set on your liquidity concentration ranges in KyberSwap Elastic. These options correspond to the relative price correlation between token pairs and the full list can be found [here](user-guides/elastic-pool-creation.md#fee-tier-options).

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

<summary>How do I tell what rewards a Farming pool offers?</summary>

To incentivize yield farming on our platform, we usually offer KNC token as a reward for staking activity in our active farming pools. From time to time we also jointly offer other tokens with our partners as staking rewards. You can easily tell which active farming pools offer KNC or KNC and another token when you look at the pool details in list view. Select the list view icon on the Active farms page to toggle this view.

<img src="https://support.kyberswap.com/hc/article_attachments/14216593542425" alt="001_FarmsListView.png" data-size="original">

From here you can see the types of coins offered under the “My Rewards” column. For example, in the following graphic, the first three farms offer both KNC and LDO as rewards, whereas the following three farms on the list offer just KNC.

<img src="https://support.kyberswap.com/hc/article_attachments/14216593573017" alt="002_MyRewardsColumn.png" data-size="original">

</details>

<details>

<summary>Is there a deadline for collecting my Yield Farming rewards?</summary>

There is no deadline for collecting (aka harvesting) your pool farm rewards. However please note that some farming pools have vesting periods: after harvesting, the rewards can only be withdrawn after a set vesting period. The vesting period counter starts at the point of collection.

</details>

<details>

<summary>How long is the vesting period for yield farming rewards?</summary>

Farming pool rewards can be withdrawn after they vest. The vesting period varies from pool to pool, with some farming pools not having a vesting period. You can check the vesting period of the farm you’re participating in by navigating to the Vesting tab on the Farms page. Note that the vesting period counter starts at the point of collection.

</details>

<details>

<summary>How secure are KyberSwap and KyberDAO?</summary>

Kyber Network highly values the security of the KyberSwap protocol and the KyberDAO governance platform.

KyberSwap is fully non-custodial and our users’ funds are not held by KyberSwap. In addition, KyberSwap, KyberDAO, and their associated smart contracts have been audited by reputable audit teams in the blockchain industry, such as [Chainsecurity](https://chainsecurity.com/) and [Hacken](https://hacken.io/).

You can refer to the [Audits](../../reference/audits.md) page for the respective reports.

</details>

Still can't find what you're looking for? Check out the [KyberSwap Help Center](https://support.kyberswap.com/hc/en-us).
