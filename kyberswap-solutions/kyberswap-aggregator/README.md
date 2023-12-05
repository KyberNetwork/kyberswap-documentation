---
description: Connecting Siloed Liquidity Across DEXs and Chains
---

# KyberSwap Aggregator

## Overview

KyberSwap Aggregator enables traders to swap at superior rates by seamlessly connecting users and applications to fractured liquidity across various decentralized exchanges and multiple chains. Through splitting and optimizing trade routes via both [AMM](../../getting-started/foundational-topics/decentralized-finance/automated-market-maker.md) and [Order Book](../../getting-started/foundational-topics/decentralized-finance/order-book.md) DEXs, KyberSwap Aggregator is able to objectively discover capital efficient liquidity sources thereby ensuring favourable swap rates while encouraging greater market stability.

For developers, KyberSwap Aggregator provides you a set of [APIs](aggregator-api-specification/) which enables you to discover the best DEXs to route your swap via a single API call. Developers integrating KyberSwap also have the option of customising fees, as well as which token they would like to accept the fees in.

{% hint style="info" %}
#### Supported exchanges and networks

For the full list of DEXs which have been integrated across KyberSwap Aggregator supported chains, please refer to [Supported Exchanges And Networks](../../getting-started/supported-exchanges-and-networks.md).
{% endhint %}

## Limit Order integration

To ensure superior rates, KyberSwap Aggregator has integrated KyberSwap [Limit Orders](../limit-order/) as an additional liquidity source. This means that swaps via the Aggregator will also be routed through active limit orders which effectively increases the pool of potential liquidity sources for an Aggregator swap. By combining solutions, KyberSwap ensures optimal rates for our users by sourcing capital efficient liquidity sources for a swap.

<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption><p>Swap routed via KyberSwap Limit Order</p></figcaption></figure>

For more info on configuring liquidity sources for your swap, please visit [Customizing Trade Parameters](broken-reference).

## Professional Market Maker Integration

In addition to the liquidity sources above, KyberSwap Aggregator has also been integrated with Professional Market Makers (PMMs) enabling Aggregator swaps on Ethereum Mainnet to access real time quotes from our network of PMMS. PMM quotes are gathered off-chain and only settled on-chain if the PMM quotes offer more favourable rates. KyberSwap's PMM network adds greater market depth to what is already an [extensive list of liquidity sources](../../getting-started/supported-exchanges-and-networks.md) ensuring superior rates for KyberSwap traders and integrators.

PMMs actively quote two sides of the markets and generate a profit based on the difference in the bid-ask spread. As a result of this market making role, PMMs are able to more efficiently deploy liquidity and consequently aid in the price discovery of an asset without the added volatility. By connecting multiple on-chain ([DEXs](../../getting-started/foundational-topics/decentralized-finance/decentralised-exchange-dex.md), [Aggregators](../../getting-started/foundational-topics/decentralized-finance/dex-aggregator.md)) and off-chain ([KyberSwap Limit Order](../limit-order/), PMMs) liquidity sources, KyberSwap not only guarantees more equitable access to capital but also actively contributes towards a more efficient market.

## Next steps

<details>

<summary>Liquidity Providers</summary>

* [Discover how KyberSwap sources more trades for your pool](concepts/dynamic-trade-routing.md)

</details>

<details>

<summary>Traders</summary>

* [Learn how KyberSwap sources the best rates for your swap](concepts/dynamic-trade-routing.md)
* [Instantly swap at superior rates from the KyberSwap Interface](broken-reference)

</details>

<details>

<summary>Developers</summary>

* [Explore key Aggregator concepts](concepts/)
* [Execute a swap with the Aggregator API](developer-guides/execute-a-swap-with-the-aggregator-api.md)
* [Filter Aggregator queries using KyberSwap DEX IDs](dex-ids.md)

</details>
