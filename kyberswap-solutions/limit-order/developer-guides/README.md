---
description: Code Samples To Get You Started
---

# Developer Guides

The guides in the following section are targeted at application developers as well as smart contract integrators that are interested in building on top of the KyberSwap Limit Orders ecosystem.

## Overview

KyberSwap Limit Orders implements a single contract for developers to interact with. The `LimitOrderProtocol` contract enables both maker (sell-side) and taker (buy-side) orders to be settled on-chain. Users commit to an order by signing an off-chain transaction which is only settled on-chain when the a matching order is sourced. Please refer to [Limit Order Contract Addresses](../contracts/limit-order-contract-addresses.md) for the full list of contracts which have been deployed across the supported chains.

## Next steps

A limit order must first be created as makers predefine the liquidity which they are willing to commit to sell in the open market. Following the creation of a limit order, takers can then fill the limit order by searching open orders and executing the trade as a counter-party.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="broken-reference"><strong>Makers - Place A Limit Order</strong></a></td><td></td><td></td><td><a href="broken-reference">Broken link</a></td></tr><tr><td><a href="broken-reference"><strong>Takers - Fill A Limit Order</strong></a></td><td></td><td></td><td><a href="broken-reference">Broken link</a></td></tr></tbody></table>
