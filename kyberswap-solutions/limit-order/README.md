---
description: Trade On Your Own Terms
---

# Limit Order

## Overview

![Limit Orders](https://docs.kyberswap.com/assets/images/v1\_create\_limit\_order\_2x-d813c99dc27fb49947a02c7b74c8b705.gif)

KyberSwap Limit Order was created to enable our users to trade on their own terms. This means users are able to predefine their preferred swap rates which are automatically settled on-chain by KyberSwap smart contracts when market conditions favor the trader. No more having to monitor the markets around the clock waiting for your target price. Trades are always settled when prices favor the trader, meaning that users might actually receive more tokens than expected. Critically, users have complete ownership of their assets until a matching trade has been found.

The [KyberSwap Interface](https://kyberswap.com/limit/) provides a convenient interface to easily create, modify, and track all your orders. KyberSwap has also implemented a suite of Limit Order APIs that enable developers to  seamlessly integrate limit order functionality within their apps.

KyberSwap Limit Orders support all ERC20 tokens and the full list of supported chains can be found [here](../../getting-started/supported-exchanges-and-networks.md).

{% hint style="info" %}
### Out Of Scope

_We will not provide an order book interface for users to visualize the limit order (_[_example_](https://dex.raydium.io/)_). This is something we can consider in the future_
{% endhint %}

## Next Steps

<details>

<summary>Liquidity Providers</summary>

* [Discover how limit orders are routed to your pool](concepts/off-chain-relay.md)

</details>

<details>

<summary>Traders</summary>

* [Learn how KyberSwap sources the best liquidity for your swap](concepts/off-chain-relay.md)
* [Trade at your preferred rates on the KyberSwap Interface](../kyberswap-interface/user-guides/trade-at-your-preferred-rates.md)

</details>

<details>

<summary>Developers</summary>

* [Explore key Limit Order concepts](concepts/)
* [Create an order using the Limit Order API](limit-order-api-specification/)
* [View Limit Order contract code and addresses](contracts/)

</details>
