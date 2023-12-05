---
description: Avoid The Pitfalls Of Low Liquidity
---

# Price Impact

## Overview

Price impact refers to the change in the market price that is brought about due to the execution of a transaction. Price impact is determined by the trade size relative to the available liquidity. In general, as each token purchased results in less available supply, it follows that the price of each additional token unit increases accordingly. Put simply, the more tokens demanded by a trade, the higher the average price per token as tokens will have to be sourced further and further from the market price (i.e. the market price only indicates the price of the next available token).

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption><p>KyberSwap price impact</p></figcaption></figure>

As an example, the screenshot above taken from the KyberSwap [swap page](https://kyberswap.com/swap) indicates that a 10M USDC to USDT trade would result in a 14.65% price impact. This means that such a trade would result in the trader paying, on average, 14.65% more USDC per USDT token as compared to the current market price.

As price impact is a function of supply and demand, it is a natural outcome of any market. As such, it is important to be aware of the price impact of your trades and take the necessary steps to minimize it.&#x20;

{% hint style="info" %}
#### Slippage vs price impact

Although closely related, slippage and price impact are separate concepts. Slippage occurs due to market factors external to the trader while price impact occurs due to the size of a trade relative to the available liquidity.

Please refer to the [Slippage](slippage.md) page for more details.
{% endhint %}

## DEX price impact

Due to the varying [DEX ](decentralised-exchange-dex.md)order matching mechanisms, price impact tends to be more pronounced for users on [AMM DEXs](automated-market-maker.md) as opposed to [order book DEXs](order-book.md).

### AMM price impact

Every AMM pool maintains a ratio of tokens against which trades are made along a price curve. As a result of this design, trading against a pool means adding one token to the pool while simultaneously removing the other token. For example, if a trader swaps 1 ETH for DAI in an ETH/DAI pool, the trader is adding 1 ETH to the pool while withdrawing 1600 DAI (assuming market price of the next 1 ETH is 1600 DAI). Given that the token ratio is a key determinant of pool price, this inverse movement of token quantities results in even greater price movements as the supply of the token being bought (i.e. DAI) drops while the supply of the token being sold increases (i.e. ETH).

The AMM price curve design ensures that the price per token scales with the available liquidity in the pool. Nonetheless, this results in higher price impact risks for pools with less liquidity as prices increases exponentially for every additional token. To mitigate price impact risks, it is advisable to split large trades across different pools or you can use an aggregator (e.g. [KyberSwap Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/)) which automatically splits and reroutes trades to the most capitally efficient liquidity sources.

### Order book price impact

Price impact does not apply to order book DEXs in the conventional flow as active limit orders are only executed when a matching order is found. As such, setting a limit order that is within the bid-ask spread sidesteps any price impact risks as limit orders will be filled when the current market price matches the limit order ask. Put in another way, the "impact" that your limit order has on the market is that you are creating a price floor or ceiling for the asset.

Where price impact does come into play is when a trader sets a limit order that is significantly above or below the market price. This might happen accidentally due to mistaken input parameters or as part of more complex trading strategies to secure large amounts of tokens at predefined prices (i.e. according to active limit orders). In such cases, price impact is limited to the difference between the limit order price and the market price.&#x20;

## Protecting our users

KyberSwap's highest priority is the safety of our users. As such, we have implemented multiple safeguards to ensure that traders using our platform do not receive any unwelcomed surprises.&#x20;

By splitting and rerouting trades across multiple liquidity sources, the [KyberSwap Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/) minimizes the potential price impact incurred from any single source. Moreover, the [KyberSwap Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/) enables traders to set a `Max Slippage` to guarantee that trades are only executed if the final price is within the expected price range.

Lastly,[ KyberSwap Limit Orders](../../../kyberswap-solutions/limit-order/) will always attempt to fill active orders at the market price. KyberSwap Limit Orders have been integrated with the KyberSwap Aggregator to ensure a larger potential pool of liquidity sources which reduces the potential price impact of an order.

{% tabs %}
{% tab title="Traders" %}
* [Customizing Trade Parameters](broken-reference)
* [Instantly Swap At Superior Rates](broken-reference)
* [Swap At Your Preferred Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/trade-at-your-preferred-rates.md)
{% endtab %}

{% tab title="Developers" %}
* [Execute A Swap With The Aggregator API](../../../kyberswap-solutions/kyberswap-aggregator/developer-guides/execute-a-swap-with-the-aggregator-api.md)
* [Place A Limit Order](broken-reference)
* [Fill A Limit Order](broken-reference)
{% endtab %}
{% endtabs %}
