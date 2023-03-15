---
description: 2 Innovative Solutions, Unlimited Opportunities
---

# Classic vs Elastic

## Overview

Both Classic and Elastic are specialized [AMM](../../getting-started/foundational-topics/decentralized-finance/automated-market-maker.md) implementations which hold a pool of assets against which trades can be made against. Critically, all trades against an AMM are conducted along a smooth price curve which determines how liquidity can be efficiently utilized across various price ranges. By customizing this price curve formulas, protocols are able to maximize the risk-adjusted returns based on specific use cases. Herein lies the key difference not just between Classic and Elastic but the new generation of AMM protocols.

In addition to varying price curve implementations, both KyberSwap protocols are uniquely equipped with specialized features:

* KyberSwap Classic introduces [dynamic auto-adjusting fees](../kyberswap-classic/concepts/flexible-fee-adjustment.md) which adjusts according to the actively traded volume of the token pair. Fees are able to adjust to market volatility whereby lower fees during periods of stability encourages more trades and higher fees during volatile periods offsets impermanent loss risks.
* KyberSwap Elastic introduces a [reinvestment curve](../kyberswap-elastic/concepts/reinvestment-curve.md) which enables generated yields to be auto-compounded through reinvesting into the pool at an infinite range. Concentrated liquidity fees no longer need to be separately removed in order to be reinvested thereby maximizing capital efficiency while simultaneously reducing gas overhead.

For a more detailed overview of each protocol, you can visit the respective concepts pages which goes through all the various concepts relating to the protocol:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong></strong><a href="../kyberswap-classic/concepts/"><strong>KyberSwap Classic Concepts</strong></a><strong></strong></td><td></td><td></td><td><a href="../kyberswap-classic/concepts/">concepts</a></td></tr><tr><td><strong></strong><a href="../kyberswap-elastic/concepts/"><strong>KyberSwap Elastic Concepts</strong></a><strong></strong></td><td></td><td></td><td><a href="../kyberswap-elastic/concepts/">concepts</a></td></tr></tbody></table>

## Elastic = Aggregated Classic

At its core, an Elastic pool combines the liquidity from multiple Classic pools into a single pool. In other words, Elastic implements an aggregated Classic price curve (see [Technical Comparison](draft-technical-comparison.md)). As a LP, there are a few considerations which arises due to this design.

### Dynamic vs static fees

In Classic, dynamic fees were made possible as all liquidity was evenly distributed between the price range specified on setup. Adding liquidity to an existing Classic pool meant acknowledging the initial pool parameters were in alignment with your specific risk profile. Consequently, fees could be easily auto-compounded into the pool as liquidity in the pool was fungible.&#x20;

With the introduction of [concentrated liquidity](../kyberswap-elastic/concepts/concentrated-liquidity.md) positions in Elastic, the pool's liquidity became non-fungible as the protocol needed to actively track how much of each LP's liquidity was supporting active trades (i.e. liquidity is not evenly distributed but LP defined). Due to the significant complexity which this entails, Elastic has been implemented with static fees. Similar to static fees in Classic, the pool fee is fixed via a fee tier at the point of Elastic pool creation. This made it possible for Elastic to implement the reinvestment curve as a way to counteract the market neutral IL risks.

For traders and arbitrageurs, this means that trading fees can change according to market conditions hence this is an additional variable to keep in mind when trading against Classic pools with dynamic fees.

### Liquidity provision

Both Classic and Elastic allows LPs to configure the relative token amounts to be added to a pool on creation. However, once a Classic pool has been created, any future liquidity additions will be determined by the initial pool parameters as well as the available liquidity in the pool. This stands in contrast to Elastic pools whereby LPs are still able to specify their preferred liquidity ranges when adding to an existing pool. As an LP, this means that you are able to define your liquidity provision risks for every new Elastic position instead of having to create a new Classic pool each time.

### Position changes

The frequency of LPs updating their liquidity positions depends on a myriad of factors from market volatility to price correlation between token pairs changing over time. For LPs expecting more frequent changes to their position, Elastic might provide a better user experience as positions are updated in the same Elastic pool without having the overhead of creating a new Classic pool.

### Fee withdrawal

Unlike Classic pools where fees accrue directly to the pool's liquidity, Elastic fees are auto-compounded via a separate reinvestment curve. As such, Elastic LPs are able to withdraw the accrued fees independent of their liquidity position. Do note that due to the reinvestment curve design, LPs are required to withdraw the full amount of accrued fees when collecting their fees. To achieve a similar outcome in Classic, LPs will have to partially withdraw from their active position.

### Impermanent loss risks

Neither Classic nor Elastic has inherently more IL risks as it ultimately depends on how liquidity is distributed within a particular price range. In general, the higher the capital efficiency (i.e. liquidity distributed over narrower price range), the higher the impermanent loss risks as each price step results in more of the underlying assets being swapped. Both protocols enable liquidity to be concentrated within a narrower price range but the difference lies in where this price range sits relative to the current market price at the point of liquidity provision.

### Trade routing

As a consequence of Elastic pools being able to support multiple LPs, each with their own preferred risk profiles, the routing of a trade through the pool also becomes more straightforward as liquidity is less likely to be fragmented across different pool contracts. In Elastic, liquidity for the same token pair is split according to the fee tier of the pool with the majority of LPs likely consolidating to a specific fee tier based on the token correlation. Classic adds the additional dimension of fixed price ranges for LPs that agree on the fee tier but not the liquidity provision price range.

From a single pool perspective, it makes discovery and integration more complex but the [KyberSwap Aggregator](../../kyberswap-solutions/kyberswap-aggregator/) handles the complexity of connecting such siloed liquidity via a convenient [API](../../kyberswap-solutions/kyberswap-aggregator/aggregator-api-specification/). Traders do not have to worry about price discovery as all swaps on KyberSwap will always be routed to the most optimal liquidity sources.

### Advanced trading strategies

One trading strategy that was made viable with Elastic is that of gradual selling of assets up or down the price curve (i.e. similar to discount-cost averaging). As LPs are able to define a custom price range, it becomes possible for such a position to be used as a gradual buy/sell strategy instead. From this perspective, the LP which is planning to sell their assets will be able to benefit from a gradual sell-down of his assets as well as any LP fees that might have accrued to his position.

While the above is also possible in Classic, the lack of fine-tuned price adjustments makes it more difficult for traders to consistently update their price ranges. This is because each change requires a new Classic pool to be created as opposed to a single position in the same Elastic pool.

### Composability

As the majority of AMMs have adopted the simpler fungible liquidity setup, Classic has a distinct advantage when it comes to composability due to the existing tools and interfaces. Given Elastic's novelty, its more complex non-fungible liquidity structure requires a more advanced toolset. Moreover, Elastic concepts was built on top of Classic hence developers integrating with Elastic requires more specialized knowledge. To this end, we are constantly improving our [KyberSwap Elastic docs](../kyberswap-elastic/) as we believe that users still stand to benefit from concentrated liquidity solutions.
