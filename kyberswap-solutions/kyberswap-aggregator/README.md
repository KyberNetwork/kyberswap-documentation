---
description: Connecting Siloed Liquidity Across DEXs and Chains
---

# KyberSwap Aggregator

## Overview

KyberSwap Aggregator enables traders to swap at the best rates by seamlessly connecting users and applications to fractured liquidity across various decentralized exchanges and multiple chains. Through splitting and optimizing trade routes via both [AMM](../../getting-started/foundational-topics/decentralized-finance/automated-market-maker.md) and [Order Book](../../getting-started/foundational-topics/decentralized-finance/order-book.md) DEXs, KyberSwap Aggregator is able to objectively discover the most capital efficient liquidity sources thereby ensuring the best swap rates while encouraging greater market stability.

For developers, KyberSwap Aggregator provides you a set of [APIs](aggregator-api-specification/) which enables you to discover the best DEXs to route your swap via a single API call. Developers integrating KyberSwap also have the option of customising fees, as well as which token they would like to accept the fees in.

{% hint style="info" %}
#### Supported exchanges and networks

For the full list of DEXs which have been integrated across KyberSwap Aggregator supported chains, please refer to [Supported Exchanges And Networks](../../getting-started/supported-exchanges-and-networks.md).
{% endhint %}

## Limit Order integration

To ensure the best rates, KyberSwap Aggregator has integrated KyberSwap [Limit Orders](../limit-order/) as an additional liquidity source. This means that swaps via the Aggregator will also be routed through active limit orders which effectively increases the pool of potential liquidity sources for an Aggregator swap. By combining solutions, KyberSwap ensures the best rates for our users by sourcing the most capital efficient liquidity for a swap.

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Swap routed via KyberSwap Limit Order</p></figcaption></figure>

For more info on configuring liquidity sources for your swap, please visit [Customizing Trade Parameters](../kyberswap-interface/user-guides/instantly-swap-at-the-best-rates.md#customizing-trade-parameters).

## Next steps

<details>

<summary>Liquidity Providers</summary>

* [Discover how KyberSwap sources more trades for your pool](concepts/dynamic-trade-routing.md)

</details>

<details>

<summary>Traders</summary>

* [Learn how KyberSwap sources the best rates for your swap](concepts/dynamic-trade-routing.md)
* [Instantly swap at the best rates from the KyberSwap Interface](../kyberswap-interface/user-guides/instantly-swap-at-the-best-rates.md)

</details>

<details>

<summary>Developers</summary>

* [Explore key Aggregator concepts](concepts/)
* [Execute a swap with the Aggregator API](developer-guides/execute-a-swap-with-the-aggregator-api.md)
* [Filter Aggregator queries using KyberSwap DEX IDs](dex-ids.md)

</details>
