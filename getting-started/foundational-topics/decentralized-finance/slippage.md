---
description: Securing Your Trades Against Market Fluctuations
---

# Slippage

## Overview

Slippage refers to the difference between the expected and final price of a trade. As there is always a certain amount of time between order placement and order execution, there is a possibility that market conditions might have changed during this short interval. Consequently, time to execution is a significant factor when considering slippage risks. By extension, slippage risks are also higher during periods of relative market volatility whereby asset prices tend to change more rapidly.

It is important to note that slippage is an inherent characteristic of any active market. As such, it is important to be aware of how it can affect your trades and what are the steps you can take to mitigate its effects. Of note, slippage is not always negative as it could also result in more favorable trades which we will cover in more detail below.

{% hint style="info" %}
#### Slippage vs price impact

Although closely related, slippage and price impact are separate concepts. Slippage occurs due to market factors external to the trader while price impact occurs due to the size of a trade relative to the available liquidity.

Please refer to the [Price Impact](price-impact.md) page for more details.
{% endhint %}

## DEX slippage

Specific to DeFi, the majority of trades take place via [DEXs](decentralised-exchange-dex.md) hence slippage presents itself differently depending on the order matching mechanism.&#x20;

Note that for public blockchains, transactions are always batched into their respective blocks to be appended to the chain. This means that the slippage window increases according to how your transaction is prioritized by the network. Moreover, even within the same block, it is possible that trades for the same token pair are ordered before yours. As such, DEXs have implemented various safety mechanisms in an effort to minimize any unexpected trading outcomes.

### AMM slippage

For [AMM DEXs](automated-market-maker.md), trades occur along a smooth price curve hence every trade against the pool will shift the market price according to the resulting token ratio changes in the pool. In the event that another transaction against the target pool is prioritized over yours, the actual price of the pool would have changed between the confirmation of your order and the final execution.&#x20;

Due to how orders are prioritized on the blockchain (see above), it is not possible to guarantee the price at the point of order submission. As such, rather than failing the order which would result in an endless cascade of failed orders, most AMMs have implemented a slippage tolerance parameter  for trades against their pools. By setting the slippage as a percentage of the expected price, transactions can still be executed as long as the final price is within the boundaries set. This makes  transaction processing much more efficient at the application layer while also enabling traders to protect their trades.

While it is always recommended to keep the slippage setting as low as possible to ensure trades are executed at the best rates, such transactions might face a higher failure rate in times of extreme market volatility. Setting a higher slippage increases the likelihood of transaction success but comes with greater risks of worse rates due to market volatility as well as the presence of front-running opportunities.&#x20;

## Order book slippage

For [order book DEXs](order-book.md), trades are executed when a pending order is filled by a counterparty with a matching order. In the case of limit orders where trades are only executed if the market price matches the expected price, hence slippage only happens in the direction favouring the trader. As such, limit orders are a great way to ensure that there are no negative trade outcomes based on the predefined parameters of the trade.

As limit orders can be valid for an indefinite amount of time, order book DEXs have also implemented an expiry and cancellation mechanism for limit orders. This acts as a safety mechanism so that traders are able to act according to the changing market conditions and not be caught with unfavorable orders which they had committed to under different market conditions.

## Positive vs negative slippage

As hinted above, slippage can be either negative or positive as its definition does not specify a particular direction in terms of expected and executed price. As a user in the DeFi space, it is usually harder to realize positive slippage due to the presence of [MEV](maximal-extractable-value-mev.md) bots which are always on the lookout for front-running opportunities. This is especially the case for larger trades where the gas costs required for a successful MEV strategy becomes progressively more insignificant as the trade size increases.

## Protecting our users

KyberSwap's highest priority is the safety of our users. As such, we have implemented multiple safeguards to ensure that traders using our platform do not receive any unwelcome surprises.&#x20;

By splitting and rerouting trades across multiple liquidity sources, the [KyberSwap Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/) minimizes the potential slippage incurred from any single source. Moreover, the [KyberSwap Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/) enables traders to set a `Max Slippage` to guarantee that trades are only executed if the final price is within the expected price range.

Lastly, [KyberSwap Limit Order](../../../kyberswap-solutions/limit-order/) allows traders predefine the prices at which their trades will be executed. This sidesteps any negative slippage risks and provides traders much greater price guarantees for their trades.

{% tabs %}
{% tab title="Traders" %}
* [Customizing Trade Parameters](../../../kyberswap-solutions/kyberswap-interface/user-guides/instantly-swap-at-the-best-rates.md#customizing-trade-parameters)
* [Instantly Swap At The Best Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/instantly-swap-at-the-best-rates.md)
* [Swap At Your Preferred Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/trade-at-your-preferred-rates.md)
{% endtab %}

{% tab title="Developers" %}
* [Execute A Swap With The Aggregator API](../../../kyberswap-solutions/kyberswap-aggregator/developer-guides/execute-a-swap-with-the-aggregator-api.md)
* [Place A Limit Order](../../../kyberswap-solutions/limit-order/developer-guides/place-a-limit-order.md)
* [Fill A Limit Order](../../../kyberswap-solutions/limit-order/developer-guides/fill-a-limit-order.md)
{% endtab %}
{% endtabs %}
