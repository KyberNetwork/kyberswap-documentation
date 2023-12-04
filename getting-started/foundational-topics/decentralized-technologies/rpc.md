---
description: Connecting Dapps To The Blockchain
---

# RPC

## Overview

In the Web3 space, a RPC is a shorthand which generally refers to how a [dapp](dapps.md) gets data from a blockchain. While data is transparently stored on the blockchain, querying and sorting the publicly available data is highly resource intensive. Moreover, given the immediacy of on-chain data, performance requirements usually dictate that transaction logic be computed on a full node which holds the full transaction history of the blockchain. As dapps are meant to be lightweight pieces of code that can conveniently run on a web-page or mobile browser, this approach is infeasible and that is where RPCs come in handy.

To achieve a better user experience for Web3 users, RPCs enable the following to be functionally separated:

* Dapps handle user interactions whereby users can view blockchain data and update such data by providing a signed instruction. Dapps do not need to hold onto all the blockchain data nor have the necessary computing resources to execute the transaction. As such, users can easily access dapps from any device with minimal concerns about hardware or network requirements.
* RPC nodes essentially run blockchain software and are therefore required to hold onto the full set of blockchain data and be able to reliably execute transactions. This requires significantly more computing resources and specialized hardware. By exposing an endpoint, RPC nodes enable dapps to query on-chain data as well as send signed instructions to be executed by the RPC node.

In short, RPCs allow dapps to focus on user interactions while leaving the complexity of translating and executing such user data to a node. Note that for simplicity, the above does not differentiate between the different types of nodes (i.e. light nodes, full nodes, etc.).

## RPC: Protocol, Nodes, Endpoints

From a technical standpoint, a RPC actually refers to a Remote Procedure Call protocol but this distinction is usually overlooked for end user simplicity. For the purposes of accuracy, the differences are highlighted below:

* Remote Procedure Call protocol is a standard interface which allows for a client (i.e. dapp) to remotely request for a server's (i.e. nodes) resources without requiring details on the server's location or network.
* Remote Procedure Call nodes are the servers which receive the requests from the client (i.e. dapp) and compute the instructions by runnning the blockchain software.
* Remote Procedure Call endpoints are the addresses which allows a client (i.e. dapp) to interface directly with the server (i.e. node)

In the large majority of cases, the term RPC is usually used to refer to the RPC endpoint which a user will interact with. Underlying this endpoint will of course be a RPC node which has been abstracted away.

## Selecting a RPC

As each chain requires nodes to run a different set of blockchain software, users will have to change their connected RPC endpoint when switching between chains. You can refer to our [Switching Networks guide](../../../kyberswap-solutions/kyberswap-interface/user-guides/selecting-preferred-network.md) on how to achieve this.

In addition to switching between chains, there is also an element of trust when a user selects a specific RPC on a chain. This is because the execution of dapp logic ultimately depends on the RPC node reliably and objectively processing the signed instructions. A RPC which is consistently offline or slower to respond would result in a degraded user experience. Moreover, RPC nodes can even take advantage of the transaction data to execute [MEV strategies](../decentralized-finance/maximal-extractable-value-mev.md) thereby profiting at the expense of the user. As such, users will have to select RPCs based on a combination of factors.

{% hint style="success" %}
#### MEV Protection

KyberSwap allows users to select RPCs which protect the user's transactions against MEV strategies by routing the transaction into a private mempool. Please refer to MEV protection for more details.
{% endhint %}
