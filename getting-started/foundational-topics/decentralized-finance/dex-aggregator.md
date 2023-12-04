---
description: DeFi's Liquidity Backbone
---

# DEX Aggregator

## Fractured liquidity

While [DEXs ](decentralised-exchange-dex.md)managed to achieve the non-trivial goal of facilitating secured and pseudonymous peer-to-peer transactions, a more socioeconomic challenge arose due to the open and permissionless nature of DeFi. Given that public smart contract code could easily be copied and tweaked, liquidity for the same asset pairs were fractured across various DEXes for a myriad of reasons:

* **Transaction costs**: The network fees (gas) that was required to confirm a transaction could make smaller volume trades unprofitable. Users who prioritize lower fees might migrate their trades to DEXs on a chain with lower transaction fees.
* **Yield optimisation**: Various [AMM DEXs](automated-market-maker.md) implemented customised pricing curves in an effort to maximise a liquidity provider’s risk-adjusted returns. Liquidity providers have different risk profiles resulting in each provider having a preferred DEX implementation. This is less significant for [order book DEXs](order-book.md) as users define their own risk levels through manual market making.
* **Information asymmetry**: Given DeFi ecosystem maturity, information on the best rates are not easily available resulting in more partially informed decisions.
* **UX familiarity**: Doing your own research (DYOR) takes a significant amount of time and hence users will tend to gravitate towards [dapps](broken-reference) which they are more familiar with, even if the rates offered are objectively sub-par.
* **Ecosystem considerations**: DEXs forms a part of a larger DeFi ecosystem hence there are other non-DEX specific considerations such as preferred tokens, integration with other DeFi primitives, etc.

Due to the above reasons, liquidity tends to be fractured across individual DEXs resulting in less optimal trades and yields. For order book DEXs, the splitting of trade orders results in shallower book depth and therefore less likelihood that a pending order will be matched. For AMM DEXs, the splitting of liquidity meant that the relative size of a trade against a liquidity pool was larger, resulting in greater slippage. Consequently, there exists a strong incentive for DEXs to engage in anti-competitive behaviour in the short term which goes against the goal of a decentralised and open DeFi ecosystem.

## Connecting siloed liquidity

DEX aggregators are a demand-side solution that was created with the purpose of connecting siloed liquidity across various DEXs (both AMM and order book). This is achieved through splitting and rerouting trades across various DEXs to achieve optimal swap rates given the network conditions. By aggregating liquidity across DEXs, aggregators provide users with a convenient entry point to explore and compare rates in an objective manner.

An aggregator’s competitive edge comes from its ability to efficiently calculate the most efficient trade route taking into account swap rates, slippage, and gas fees. Critically, this trade route optimisation necessitates programmatically routing trades towards the most capitally efficient liquidity sources which encourages greater market stability through competition.

## How DEX Aggregators work

DEX aggregators are made possible due to the open and composable nature of DeFi whereby standard interfaces enable liquidity to be queried and trades to be executed directly with a DEX smart contract. Through integration with a myriad of DEX smart contracts, aggregators are able to function as an optimisation layer between the DEX smart contract and incoming trade requests. The centralised equivalent would be similar to a brokerage/OTC rerouting trades across multiple exchanges.

The basic concept behind aggregators is quite simple and consists of the following generalised steps:

1. User submits a swap request to the aggregator API endpoint.
2. The aggregator queries the connected DEXs for liquidity data on the specified trading pair. _Note that token standards (i.e._ [_ERC20_](tokens.md#token-standards)_) ensures token interoperability across DEXs._
3. Based on the trade volume, the aggregator will calculate a more efficient route for the trade using the aggregated liquidity data. Trades might even be split if the potential slippage outweighs the gas costs.
4. Bundle the trade route(s) as an unsigned transaction pending the user’s approval.
5. User views the finalised trade route and submits a signed transaction to the network, using a network provider of their choice.
6. An aggregator smart contract atomically executes the signed transaction, debiting the user’s input token.
7. User receives the output token in their account.

In keeping with DeFi composability, notice that aggregators do not specify a particular user interface implementation nor infrastructure communication channels (i.e. providers). While many aggregator teams have implemented their own user interface (eg. [Kyberswap Interface](../../../kyberswap-solutions/kyberswap-interface/)) for users to view and submit trades, the aggregator API endpoint can be easily triggered from any web application. Aggregators can therefore be seamlessly integrated with applications demanding superior token swap rates without the overhead of managing multiple liquidity sources.

Note that the bundled transactions should also be atomically executed by the network. This ensures that trades with multiple routes do not get partially settled which could result in an overall disadvantageous position as the network condition dynamically changes. Transaction atomicity provides greater assurances around the final swap price which would always be within the user consented interval.

A key aspect to this flow is that users are given the final option to consent to the suggested route as the bundled transaction requires their signature. While aggregators return all the details of the trade (ie. route, splits, final price), application developers are still responsible for displaying such information to the user in a way that best suites their target user. Nonetheless, having an application which provides transparent and easily understandable data will likely result in the application having a competitive edge as this aligns with the optimal user experience.

## Trade at superior rates

The[ KyberSwap Aggregator ](../../../kyberswap-solutions/kyberswap-aggregator/)can be conveniently accessed via the [KyberSwap Interface](../../../kyberswap-solutions/kyberswap-interface/). By initiating a trade via the KyberSwap [UI](https://kyberswap.com/swap), users are able to view optimal rates as well as the exact route which their trade will take.

For developers, KyberSwap Aggregator exposes a set of [swap APIs ](../../../kyberswap-solutions/kyberswap-aggregator/aggregator-api-specification/)which enable favourable rates to be queried and encoded to be sent to the [Aggregator smart contract](../../../kyberswap-solutions/kyberswap-aggregator/contracts/aggregator-contract-addresses.md).

{% tabs %}
{% tab title="Traders" %}
* [Instantly Swap At Superior Rates](broken-reference)
{% endtab %}

{% tab title="Developers" %}
* [Integrating The KyberSwap Widget](../../../kyberswap-solutions/kyberswap-widget/developer-guides/integrating-the-kyberswap-widget.md)
* [Execute A Swap With The Aggregator API](../../../kyberswap-solutions/kyberswap-aggregator/developer-guides/execute-a-swap-with-the-aggregator-api.md)
* [Aggregator API Specification](../../../kyberswap-solutions/kyberswap-aggregator/aggregator-api-specification/)
* [Aggregator Contracts](../../../kyberswap-solutions/kyberswap-aggregator/contracts/)
{% endtab %}
{% endtabs %}
