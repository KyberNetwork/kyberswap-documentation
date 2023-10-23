---
description: Code Samples To Get You Started
---

# Developer Guides

The guides in the following section are targeted at application developers as well as smart contract integrators that are interested in building on top of the KyberSwap Limit Orders ecosystem. The code samples for the guides can be found on GitHub:

{% embed url="https://github.com/KyberNetwork/ks-limit-order-API-demo/tree/main" %}

## Overview

KyberSwap Limit Orders implements a hybrid [Off-Chain Relay, On-Chain Settlement](../concepts/off-chain-relay.md) design whereby Makers pre-commit to orders off-chain and Takers execute order settlement on-chain. The KyberSwap Limit Order Service exposes a set of Maker and Taker APIs which enable gasless management of limit orders secured by the option to settle on-chain. When settling orders on-chain, KyberSwap Limit Order provides the relevant APIs required to encode the call data to be sent to the Limit Order smart contracts.

Please refer to [Limit Order Contract Addresses](../contracts/limit-order-contract-addresses.md) for the full list of contracts which have been deployed across the supported chains.

## Next steps

A limit order must first be created as makers predefine the liquidity which they are willing to commit to sell in the open market. Following the creation of a limit order, takers can then fill the limit order by searching open orders and executing the trade as a counter-party.

### Maker

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="create-limit-order.md"><strong>Create Limit Order</strong></a></td><td></td><td></td><td><a href="create-limit-order.md">create-limit-order.md</a></td></tr><tr><td><a href="gasless-cancel.md"><strong>Gasless Cancel</strong></a></td><td></td><td></td><td><a href="gasless-cancel.md">gasless-cancel.md</a></td></tr><tr><td><a href="hard-cancel.md"><strong>Hard Cancel</strong></a></td><td></td><td></td><td><a href="hard-cancel.md">hard-cancel.md</a></td></tr></tbody></table>

### Taker

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="fill-limit-order.md"><strong>Fill Limit Order</strong></a></td><td></td><td></td><td><a href="fill-limit-order.md">fill-limit-order.md</a></td></tr></tbody></table>
