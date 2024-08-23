# KyberSwap OnChain Price Service

### **Overview**

Welcome to the first-ever completely on-chain price service, designed to deliver accurate, reliable, and more tradeable price information for a wide array of tokens. In this section, we will explain the enhancements we've made to our price service and how it benefits you.



## Comparison with traditional pricing service

| The quote symbol               | - Fiat currencies (USD, EUR, GBP, AUD, etc.) - Well-known cryptocurrencies (BTC, ETH, BNB, XRP, etc.)                                                                                                                                                       | - Stablecoins (USDT, USDC). - Native tokens (ETH, BNB, MATIC, etc.).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Source of price                | - Centralized Exchanges (CEXes) involving multiple pairs with different quote tokens. - Decentralized Exchanges (DEXes) with multiple pairs and possibly across different chains.                                                                           | Decentralized Exchanges (DEXes) using multiple pairs with different quote tokens.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Type of target price           | Provides a single final price without distinguishing between buy and sell prices. This aggregated price may not reflect real on-chain liquidity, which can lead to discrepancies when attempting to execute trades on Decentralized Exchanges.              | Provides both buy and sell prices separately. Based on real on-chain liquidity, this ensures the prices are reflective of market conditions and executable in real trading scenarios, offering more accurate and trade-able prices on Decentralized Exchanges.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Network-Specific Pricing       | Typically, other services aggregate prices from multiple networks and combine them into a single price. While this approach provides an overall average, it may not accurately reflect the liquidity depth or market conditions of each individual network. | Kyberswap provides network-specific prices that vary depending on the liquidity depth of each network. This ensures that the prices you see are reflective of the actual market conditions on each network, resulting in more accurate and tradeable prices tailored to where the liquidity is most concentrated.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| The price formula              | The final price is derived from an aggregation of various sources using a predefined formula, which may be average, median, or weighted-based. The exact method can vary depending on the price service.                                                    | <p>- Utilizes a graph-based algorithm to build a graph of price from the pre-defined quote token (with a pre-defined amount) to all other tokens </p><p></p><p>+ Buy Price: Determined by finding the <code>maximum output amount</code> when converting the quote token to the target token (i.e., selling X amount of the quote token to determine the maximum amount of the target token that can be purchased). </p><p></p><p>+ Sell Price: Determined by finding the <code>minimum input amount</code> required to obtain the quote token from the target token (i.e., determining the minimum amount of the target token that needs to be sold to acquire X amount of the quote token). + After having the equation X quote token &#x3C;-> Y target token , the price of the target token is derived.</p> |
| Verification of Price Accuracy | There might be a combination of market data aggregation, cross-exchange comparisons, and advanced algorithms to ensure the accuracy of their prices. They might also implement anomaly detection and regular audits to maintain reliability.                | - When passing the debug parameter in the request, the response will contain 3 more fields: + `tracedTokens` + `tracedPools` + `tracedAmounts` These fields can be used to verify the accuracy of the price calculation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |



## The Evolution of On-chain Price Service

**Consistent and Reliable Price Calculation**

Kyberswap's on-chain price service leverages the same route-finding algorithm employed in our token swap calculations.

By reusing the Kyberswap-dex-lib CalcAmountOut functions, we ensure consistency and precision in price determination, eliminating the need for a separate price calculation formula.

**Network-Specific Pricing**

Kyberswap’s price service provides network-specific prices that vary depending on the liquidity depth of each network. On-chain price now available on all chains that Kyberswap support. Unlike other services that aggregate prices from multiple networks into a single average, Kyberswap’s approach ensures that the prices are reflective of the actual market conditions and liquidity available on each specific network. This results in more accurate and trade-able prices tailored to the unique dynamics of each network.

**Enhanced Token Coverage**

Our new system supports a broader range of tokens, allowing for more accurate price information even for less common or exotic tokens.

This improvement ensures that you can trade confidently, knowing that you have access to precise and comprehensive price data across a wide array of tokens.

**Improved Accuracy and Real-Time Updates**

Kyberswap's on-chain price service utilizes the native token's price as a reference point, sourced from reliable data providers.

By continuously updating this data **every 10 seconds**, the service ensures that the prices you see are always accurate, up-to-date, and reflective of real-time market conditions. This approach guarantees that the pricing information is as precise and tradeable as possible.



### System Components and Functionality

The Kyberswap on-chain price service is comprised of several key components, each playing a vital role in delivering accurate price information:

**Token List Management**:

* The system regularly updates the list of common tokens available for trading on Kyberswap. This ensures that a comprehensive range of tokens is consistently supported, with up-to-date pricing information.

**Price Graph Construction and Maintenance**:

* The system constructs a price graph in memory, utilizing data from various sources to calculate precise token prices. This graph is updated every 10 seconds to reflect the latest market conditions.
* Latest prices are stored in Redis, while historical snapshots are archived in a time-series database, ensuring both real-time accuracy and long-term reliability.

**API-based Price Retrieval**:

* The system efficiently handles API requests by retrieving the most recent price data stored in Redis. This enables users to obtain real-time price information, facilitating informed trading decisions.

#### **Conclusion**

This service guarantees precise, **up-to-date and the most trade-able price information**, enhancing your trading experience on Kyberswap. Enjoy more informed trading decisions and a streamlined experience with our advanced on-chain price service.

Enjoy trading on <mark style="color:green;">Kyberswap</mark>!
