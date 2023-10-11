---
description: Decentralized Trading Without The Gas Fees
---

# Gasless Cancellation

## Overview

In an effort to provide the same fee-less experience which traders are used to with CEX limit orders, KyberSwap Limit Order has been enhanced with gasless cancellation functionality:

* **Gasless Cancel**: Cancel your limit order without incurring gas fees. Upon triggering gasless cancel, users might need to wait up to 5 minutes for the cancellation to be confirmed.
* **Hard Cancel**: Instantly cancel your limit order by incurring a small prioritization gas fee. Upon triggering hard cancel, users will need to confirm the gas fee whereupon cancellation is confirmed once the transaction has been mined.

With gasless cancellation, traders can now create, modify, and cancel limit orders without ever incurring gas fees with KyberSwap Limit Orders.

## Decentralized Limit Orders&#x20;

KyberSwap Limit Orders adopts a hybrid off-chain matching and on-chain settlement model as described [here](off-chain-relay.md). While this design ensures that such limit orders can continue to be open and permissionless, one of the key tradeoffs is that the limit order protocol does not have control over the ordering of transactions.&#x20;

The KyberSwap Limit Order protocol is only able to define the trade logic with transaction ordering being determined by the underlying chain. Once a limit order is created, the signed maker transaction is distributed to our network of off-chain takers.&#x20;

### Hard Cancel

As all potential takers now have a copy of the maker transaction, the only way to guarantee cancellation is to send a cancellation transaction to the chain before an order is filled. Consequently, if any of the takers match and execute the maker transaction on-chain, the limit order will fail.

The first-come, first-serve approach above describes the **Hard Cancel** option whereby makers with an open limit order pay a gas fee to ensure that their order is immediately nullified on-chain. This gas fee essentially incentivizes miners to prioritize the cancellation transaction over any taker order which has a lower gas fee. As such, cancellation is confirmed once the Hard Cancel order has been included into a mined block.

### Gasless Cancel

While the **Hard Cancel** mechanism above practically guarantees cancellation, the transaction costs accrued can quickly accumulate especially for traders who constantly make adjustments to their limit orders. In addition, the cost of a single cancellation on chains such as Ethereum Mainnet (ChainID: 1) can be prohibitively expensive especially when order sizes are small or if a wrong parameter was entered. To address these issues, a **Gasless Cancel** option was introduced.

In contrast to the **Hard Cancel** option which cancels orders on-chain, the **Gasless Cancel** option cancels the order off-chain by introducing an operator timed signature requirement. For a limit order to be valid, it must be signed by both the maker and a KyberSwap Operator, each with their own signature validity period:

* **Maker signature**: Defines the expiry for the LO. This is set by the Maker at the point of LO creation. Maker order is automatically expired after this date.
* **Operator signature**: Valid for 5 minutes and is only created when an operator unsigned maker order is included in a quote (via [LO Taker](../limit-order-api-specification/taker-apis.md) or [Aggregator](../../kyberswap-aggregator/aggregator-api-specification/evm-swaps.md) APIs).&#x20;

As a result of the aforementioned design, maker limit orders will have a maximum 5 minute validity period upon which another Operator signature is required. Consequently, maker's have the option to instruct the KyberSwap Operator not to renew their signature by submitting a **Gasless Cancel** order prior to the next Operator signature (i.e. when the maker order is requested in a quote).&#x20;

This means that, in the majority of cases, makers are able to gaslessly cancel their transactions immediately unless their maker order was previously included in a quote. In the latter case, there is a maximum 5 minute waiting period for the limit order to be cancelled off-chain.

## Choose your trading journey

KyberSwap Limit Order makers now have the option to cancel their orders depending on their specific trading requirements. For makers where gas costs are a top priority, the **Gasless Cancel** option enables limit order to be cancelled as long as they are willing to wait up till a maximum of 5 minutes for cancellation. For makers who prioritize instant cancellation, the **Hard Cancel** option enables their orders to be cancelled immediately for a small fee.
