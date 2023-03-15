---
description: Sourcing The Best Liquidity For Your Trade
---

# Dynamic Trade Routing

KyberSwap Aggregator has Dynamic Trade Routing, which aggregates fractured liquidity across DEXs and thereby enables users to source the most capitally efficient liquidity to support their trades. Through integration with a myriad of DEX smart contracts, KyberSwap Aggregator is able to function as an optimisation layer between the DEX smart contract and incoming trade requests. This ensures that users always get the best rates for any token swap, on any of the KyberSwap Aggregator supported networks.

KyberSwap trades are split and routed through different DEXs for the best prices within the same chain/network. Users can trade tokens that may not be in KyberSwap pools but are available on other DEXs. You can see exactly which DEXs were involved in the trade and the % split between them.

KyberSwap's DEX aggregator also provides the following benefits:

* **Optimised Trade Route**: If a trade only passes through KyberSwap’s own pools, the gas fees associated with this trade will be minimal. The gas fees charged to our users will be as if the DEX aggregator was not used at all.
* **Reduced Gas Fees**: We reduce the number of transfers. Therefore, the gas fees associated with trading Fee on Transfer (FoT) tokens are also reduced. _In Fee on Transfer tokens, generally, a small portion of every transfer is either burnt or diverted to another wallet (i.e. tax). FoT tokens are common on the BSC chain._
