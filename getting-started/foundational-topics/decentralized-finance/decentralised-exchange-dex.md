---
description: Non-Custodial Token Swaps
---

# Decentralized Exchange (DEX)

## Overview

Decentralised exchanges (DEXs) enables peer-to-peer trading of tokens without the custodial requirements of a middleman (i.e. a trusted third-party has to hold both assets to successfully facilitate a trade). DEXs allow users to trade directly with smart contract code with no intermediaries. The smart contract code will be viewable by anyone and all interactions with the contract will be viewable on a public blockchain (see [KyberSwap Classic Contracts](../../../liquidity-solutions/kyberswap-classic/contracts/classic-contract-addresses.md) and [KyberSwap Elastic Contracts](../../../liquidity-solutions/kyberswap-elastic/contracts/elastic-contract-addresses.md) as an example). Throughout this whole process, the user never loses custody of their own assets.

## Types of DEXs

DEXs come in two flavors which are differentiated based on their order matching mechanisms which are further detailed in their respective pages:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="order-book.md"><strong>Order Book DEX</strong></a></td><td></td><td></td><td><a href="order-book.md">order-book.md</a></td></tr><tr><td><a href="automated-market-maker.md"><strong>Automated Market Maker (AMM) DEX</strong></a></td><td></td><td></td><td><a href="automated-market-maker.md">automated-market-maker.md</a></td></tr></tbody></table>

For the purpose of this comparison, the table below summarizes the pros and cons of each according to three main convenience factors:

<table><thead><tr><th width="113.33333333333331"></th><th>Order Book</th><th>Automated Market Maker</th></tr></thead><tbody><tr><td>Price</td><td><ul><li>Price is predefined at the point of creating the order</li><li>Buyer and Seller needs to agree on a final price</li><li>Market price is the last traded price</li><li>Liquidity distribution tends to result in progressively bigger price steps as price deviates further from market price</li></ul></td><td><ul><li>Price derived from combination of trade size, pool size, and external market price</li><li>Indicative price pulled in real time based on the price curve</li><li>Final price determined via the price curve at point of trade execution</li><li>User is able to indicate a slippage tolerance where the trade will fail if the unit price falls outside these bounds</li><li>Liquidity is evenly distributed within specific price intervals</li></ul></td></tr><tr><td>Quantity</td><td><ul><li>Limited to quantity where buy price is greater than sell price</li><li>Results in market depth where available quantity increases exponentially as price deviates further from market price</li></ul></td><td><ul><li>Limited to available funds in the pool</li><li>In newer AMM versions, liquidity tends to be concentrated around the market price resulting in greater capital efficiency</li></ul></td></tr><tr><td>Time</td><td><ul><li>Sell orders require a matching buy order to be made before execution takes place</li><li>Users are able to specify an order validity period</li></ul></td><td><ul><li>Transaction finality depends on the gas premium which the user is willing to pay for their transaction to be prioritized</li></ul></td></tr></tbody></table>

## Which is better for traders?

For traders, the choice of which DEX type to use boils down to two main factors:&#x20;

### **Price assurance**

Price assurance refers to the certainty surrounding the final price of a trade. For traders prioritizing price assurance, the order book model is the better choice as it allows users to predefine a price for the trade which will be completed as long as there is a corresponding matching order. The trade will be completed when there is sufficient quantity to match the trade order.

The trade off here is that the order can take an indefinite amount of time to complete. The larger the trade volume, the longer the waiting time. Users are able to set a validity period for their order whereupon hitting the specified deadline, the order becomes invalidated.

### **Trade immediacy**

Trade immediacy refers to how quickly a trade can be executed. For traders prioritizing trade immediacy, AMM is the better choice as it allows for the trade to take place immediately without having to wait for a counter party. There are also less limits around the trade volume as the trade is against the pool's liquidity rather than an aggregation of multiple orders. Consequently, there is also less slippage risk (difference between the expected price of a trade and the price at which the trade is executed) as the price follows a smooth price curve.

The trade off here is that the trade must be executed around the current market price. The larger the trade volume relative to pool size, the further the execution price from the market price. Users are able to set a slippage tolerance but not a fixed price. The trade will be cancelled if its parameters falls outside these price boundaries.

### Which is better for market makers?

For market makers, the decision can be broken down into the following two main factors:

### Management overhead

As per its name, AMMs automates the whole market making process meaning that liquidity providers do not need to constantly monitor and readjust their positions. The liquidity provided to an AMM is constantly being utilized in the market making process according to the parameters set out in the pool. In the majority of cases, the trading fees are natively reinvested into the pool enabling yields to be compounded automatically.

The downside here is that liquidity providers have less fine tuned control over the prices which their assets are getting sold at. As long as their liquidity is supporting trades within a price range, their funds are actively being sold in incremental amounts based on the price curve.&#x20;

### Market spreads

As most AMMs (not [KyberSwap Classic](../../../liquidity-solutions/kyberswap-classic/)) implement static fees for trades, the market spread tends to be market neutral regardless of the market conditions. This could prove disadvantageous for liquidity providers during periods of extreme market volatility as they face even greater impermanent loss risks.

Limit orders enable users to manually set a price hence market spreads are implicitly accounted for  at the point of creating the order. This facilitates more fine tuned control over the trading of funds as prices are guaranteed and limit orders are less affected by the need to time the market.

## Choose your preferred journey

KyberSwap understands that market conditions can change rapidly and we want to provide our users with all the tools necessary to take advantage of the market. To this end, we have implemented multiple solutions that enable our users to trade and earn at the best rates.

{% tabs %}
{% tab title="Liquidity Providers" %}
* [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
* [Swap At Your Preferred Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/trade-at-your-preferred-rates.md)
{% endtab %}

{% tab title="Traders" %}
* [Instantly Swap At Superior Rates](broken-reference)
* [Swap At Your Preferred Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/trade-at-your-preferred-rates.md)
{% endtab %}

{% tab title="Developers" %}
* [Integrating The KyberSwap Widget](../../../kyberswap-solutions/kyberswap-widget/developer-guides/integrating-the-kyberswap-widget.md)
* [Execute A Swap With The Aggregator API](../../../kyberswap-solutions/kyberswap-aggregator/developer-guides/execute-a-swap-with-the-aggregator-api.md)
* [Place A Limit Order](broken-reference)
* [Fill A Limit Order](broken-reference)
{% endtab %}
{% endtabs %}
