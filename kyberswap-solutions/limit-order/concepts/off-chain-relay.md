---
description: Gas Efficient Pre-committed Limit Orders
---

# Off-Chain Relay, On-Chain Settlement

## Overview

The very first iterations of DeFi limit orders consisted of fully on-chain contracts whereby limit orders were stored on the blockchain itself. While this guaranteed the safety of the limit order (i.e. the order could not be tampered with or manipulated once submitted), orderbook DEXs failed to achieve the same traction as their AMM counterparts largely due to a single reason: gas costs. As every on-chain action requires gas fees, managing active limit orders can become extremely costly especially in times of extreme market volatility.

To get around this limitation, KyberSwap Limit Order implements a hybrid solution whereby limit orders are stored on an off-chain relay and only settled on-chain when a matching order has been found. The safety of the transaction is still guaranteed as traders had to commit to their limit order by signing the transaction with their private keys. This signature proves the trader's consent while also ensuring that submitted limit order can not be modified without the order being nullified.

As a result of this design, makers are able to create and pre-commit to limit orders without incurring gas fees. These orders are then stored on an off-chain orderbook from which takers are able to view the active pending orders. Upon finding a desirable limit order, takers are able to fetch the order and perform the trade by filling the order on-chain.

Note that limit order cancellations are on-chain and therefore incur a gas fee. This is because, once a limit order is created, the signed maker transaction is distributed to our network of off-chain takers. As all potential takers now have a copy of the maker transaction, the only way to guarantee cancellation is to send a cancellation transaction to the chain so that if any other takers match and execute the maker transaction on-chain, the limit order will fail.
