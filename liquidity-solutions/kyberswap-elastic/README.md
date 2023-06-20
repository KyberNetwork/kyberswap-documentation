---
description: Customized Liquidity Positions With Auto-Compounding Yields
---

# KyberSwap Elastic

## Overview

As the AMM space matured, increasingly sophisticated yield generation strategies created a strong demand for customized liquidity positions whereby liquidity providers were able to specify a price range for their liquidity positions. To meet this demand, we launched KyberSwap Elastic which iterated upon the [capital amplification](../kyberswap-classic/) capabilities of its [Classic](../kyberswap-classic/) counterpart by incorporating emerging [concentrated liquidity](concepts/concentrated-liquidity.md) concepts popularized by Uniswap V3. Through fusing the benefits of each, KyberSwap Elastic enables liquidity providers to determine their preferred liquidity price ranges while still maximizing returns through greater capital efficiency as well as the [auto-compounding of yields](concepts/reinvestment-curve.md).

Through these improved LP incentives, KyberSwap Elastic is also able to further reduce slippage for traders as market forces will incentivize liquidity to be concentrated within the most actively traded price ranges. LPs are able to compound their finely tuned risk-adjusted returns while simultaneously encouraging greater market stability through reduced slippage risks for traders.

{% hint style="info" %}
#### Elastic Legacy

On 17 April 2023, KyberSwap validated a vulnerability reported by a whitehat hacker which could result in double-counting of liquidity deposits under a specific condition. Elastic pools and farms were paused with all user funds being safely withdrawn from the identified contracts. If you still have funds in Elastic Legacy, please refer to [Remove Elastic Legacy Liquidity](../../reference/legacy/elastic-legacy/remove-elastic-legacy-liquidity.md) for a guide on how to retrieve your funds.

As of 25 May 2023, all the relevant Elastic protocol and farm contracts have been updated to fix this. Please refer to [Elastic Legacy](../../reference/legacy/elastic-legacy/) for more details.
{% endhint %}

## Next Steps

<details>

<summary>Liquidity Providers</summary>

* [Learn how price ranges affect your yield](concepts/concentrated-liquidity.md)
* [Discover how your yields are being compounded](concepts/reinvestment-curve.md)
* [Understand how Elastic protects you from front runners](concepts/anti-sniping-mechanism.md)
* [Create your own Elastic pool](user-guides/elastic-pool-creation.md)
* [Contribute liquidity to an existing Elastic pool](../kyberswap-classic/user-guides/add-liquidity-to-an-existing-classic-pool.md)
* [Receive additional rewards by yield farming on Elastic](user-guides/yield-farming-on-elastic.md)

</details>

<details>

<summary>Traders</summary>

* [Learn how Elastic APR is calculated](concepts/apr-calculations.md)
* [Get superior rates via the integrated KyberSwap Aggregator](../../kyberswap-solutions/kyberswap-interface/user-guides/instantly-swap-at-the-best-rates.md)

</details>

<details>

<summary>Developers</summary>

* [Explore key Elastic concepts](concepts/)
* [Execute a swap against Elastic pools](developer-guides/execute-an-elastic-swap.md)
* [View Elastic contract code and addresses](contracts/)

</details>
