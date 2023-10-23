---
description: Hybrid Limit Order Solution
---

# Order Book DEX

## Overview

Order book DEXs matches trades by aggregating all user specified buy and sell orders for an asset pair into an order book list. Through the creation of a buy and sell order list, potential trades can be identified through comparing matching buy and sell orders. In this case, liquidity is generated through the submission of potential trade orders which are executed when a matching trade is found.

Specific to DeFi order book implementations, such DEXs will usually require users to commit to their order by signing a transaction which is only submitted to the limit order smart contract upon a matching order being found. Orders are distributed across a network of counter-parties who will execute and fill the order by submitting a matching buy order. This ensures that funds can’t be double-spent while avoiding the hefty gas fees required for constant manual adjustment of orders. Critically, order book DEX liquidity relies on having a deep order book consisting of user defined orders.

## Trade on your own terms

[KyberSwap Limit Order](../../../kyberswap-solutions/limit-order/) enables users to predefine their preferred swap rates which are automatically settled on-chain by KyberSwap smart contracts when market conditions favor the trader. With KyberSwap Limit Orders, you can easily [Swap At Your Preferred Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/trade-at-your-preferred-rates.md).

For developers, KyberSwap Limit Order exposes a [set of APIs](../../../kyberswap-solutions/limit-order/limit-order-api-specification/) that enables you to make and take limit orders straight from your app.

{% tabs %}
{% tab title="Makers" %}
* [Swap At Your Preferred Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/trade-at-your-preferred-rates.md)
{% endtab %}

{% tab title="Traders" %}
* [Swap At Your Preferred Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/trade-at-your-preferred-rates.md)
{% endtab %}

{% tab title="Developers" %}
* [Place A Limit Order](broken-reference)
* [Fill A Limit Order](broken-reference)
* [Limit Order API Specification](../../../kyberswap-solutions/limit-order/limit-order-api-specification/)
* [Limit Order Contract Addresses](../../../kyberswap-solutions/limit-order/contracts/limit-order-contract-addresses.md)
{% endtab %}
{% endtabs %}
