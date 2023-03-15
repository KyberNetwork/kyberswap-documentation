---
description: Automating The Market Making Process Through Code
---

# Automated Market Maker DEX

## Overview

Per its namesake, AMM DEXs maintains a liquidity pool of assets against which trades can be made automatically along a pricing curve. Asset holders are incentivised to provide their tokens to the liquidity pool smart contract in exchange for a portion of the trading fees. In this case, AMM liquidity is generated when token holders lock their tokens in a liquidity pool in exchange for a percentage return on their assets. Generally speaking, the more liquidity locked in a pool, the larger the pool size relative to a trade which results in lesser slippage.

In the pursuit of greater capital efficiency, many AMMs have also implemented their own price curve formulas that enable more fine-grained tuning of liquidity flows. These specialised price curves enable users or the protocol to concentrate liquidity within a particular price interval based on specific use cases. Critically, the price curve is bounded by the pool’s total liquidity and therefore AMM DEX liquidity is heavily reliant on liquidity provider incentives.

## Concepts

As this liquidity solution involved the creation of a fundamentally different market, it required multiple concepts to be stacked on top of each other:

* Create a pool of assets against which trades can be made for a small fee. The composition of this basket of assets will be determined by the trades that are taking place against it. Arbitrageurs will play a key role in rebalancing this pool with the wider market.
* Create a price curve for the pool which ingests price data from a reliable external source. The exact price for a trade being done against the pool will take into account the external price feed, the current pool composition, as well as resulting effect the trade will have on the pool's liquidity.
* Incentivize asset holders to provide their assets to the pool via a percentage return on their assets. The majority of the trading fee which the pool charges will be accrued to the pool. This is also to sufficiently compensate the asset holder for locking up their asset with the pool and becoming a liquidity provider (LP).
* Mint new derivative tokens to the LPs’ wallet which will allow reclaiming of their assets as well as any fees which have accrued to the pool. These LP tokens represent a proportion of the pooled assets and can themselves be traded.

Taken as a whole, this solution came to be known as the **Automated Market Maker (AMM).** “Automated” because it is always available for trading and does not depend on the traditional interaction between buyers and sellers where orders must first be submitted (i.e. [orderbook model](order-book.md)).

## Trade and earn at the best rates

KyberSwap implements two AMM variants, [KyberSwap Classic](../../../liquidity-solutions/kyberswap-elastic/) and [KyberSwap Elastic](../../../liquidity-solutions/kyberswap-elastic/), which provides LPs multiple options for generating yield. For traders, [KyberSwap Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/) abstracts the complexity of searching for the best pools by conveniently splitting and routing your trade across pools with the most optimal liquidity.

{% tabs %}
{% tab title="Liquidity Providers" %}
* [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
* [Classic vs Elastic](../../../liquidity-solutions/classic-vs-elastic/)
{% endtab %}

{% tab title="Traders" %}
* [Instantly Swap At The Best Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/instantly-swap-at-the-best-rates.md)
{% endtab %}

{% tab title="Developers" %}
* [Integrating The KyberSwap Widget](../../../kyberswap-solutions/kyberswap-widget/developer-guides/draft-integrating-the-kyberswap-widget.md)
* [Execute A Swap With The Aggregator API](../../../kyberswap-solutions/kyberswap-aggregator/developer-guides/execute-a-swap-with-the-aggregator-api.md)
{% endtab %}
{% endtabs %}
