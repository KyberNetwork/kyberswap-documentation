---
description: Interacting With KyberSwap Aggregator Router Contract
---

# Execute A Swap With The Aggregator API

## Overview

KyberSwap maintains a single API specification for all EVM chains:

* [Swap API specs for EVM chains](../aggregator-api-specification/evm-swaps.md)

{% hint style="info" %}
#### KyberSwap Aggregator APIv1

Following feedback on the initial non-versioned API, KyberSwap has implemented a more performant `[V1]` API which improves the response time for getting a route via offloading encoding requirements to the post method.

For integrators who have previously integrated with the non-versioned API, please refer to [Upgrading To APIv1](upgrading-to-apiv1.md) for further details on the motivation behind the upgrade as well as the relevant changes to swap flow and parameters.&#x20;

Please use the `[V1]GET` API for more efficient route queries. The returned route can then be reused in the `[V1]POST` body to get the encoded swap data. The non-versioned`GET` and `[V1]GET` remains backwards compatible with the main change being the queried path.&#x20;

**While both versions of the API remains backwards compatible, only the `[V1]` APIs will continue to receive updates and hence developers are highly encouraged to implement the latest `[V1]` APIs to avoid any disruptions as the non-versioned API is eventually deprecated.**
{% endhint %}

## Sequence diagram

<figure><img src="../../../.gitbook/assets/Aggregator APIv1.jpg" alt=""><figcaption><p>APIv1 sequence diagram</p></figcaption></figure>

To execute a swap, the router (`MetaAggregationRouterV2`) contract requires the encoded swap data to be included as part of the transaction. This encoded swap data as well as other swap metadata are returned as part of the API response. As such, developers are expected to call the swap API prior to sending a transaction to the router contract.

{% hint style="info" %}
**Single Request Model**

While the `[V1]` APIs provide more performant queries, we understand that some integrators might prioritize a single request model over the dual request required in `[V1]`. For example, instead of querying rates and requesting for encoded data separately, both functions can be completed in a single request with slightly longer response times via our non-versioned API.

In such cases, integrators can still use our [non-versioned API](../aggregator-api-specification/evm-swaps.md#chain-route-encode) whose call parameters are similar except for an additional required `to` field that denotes the recipient of the swapped tokens. Please see [Non-versioned API swap flow](upgrading-to-apiv1.md#non-versioned-api-swap-flow) for more details.
{% endhint %}

## TypeScript Example

{% hint style="success" %}
**Aggregator API Demo**

The code snippets in the guide below have been extracted from our demo GitHub repo which showcases the full end-to-end Aggregator operations in a TypeScript environment.
{% endhint %}

{% embed url="https://github.com/KyberNetwork/ks-aggregator-api-demo/tree/master" %}

### Step 1: Query Swap Route

Integrators can easily query for superior rates by passing in the following required parameters into the [`[V1] Get Swap Route`](../aggregator-api-specification/evm-swaps.md#chain-api-v1-routes) API:

```typescript
const targetPathConfig = {
    params: {
        tokenIn: tokenIn.address,
        tokenOut: tokenOut.address,
        amountIn: Number(1*10**tokenIn.decimals).toString()
    }
};
```

[V1Get.ts](https://github.com/KyberNetwork/ks-aggregator-api-demo/blob/209a2d358fa3a47b50f87660c474d5592a155a13/src/apis/V1Get.ts#L10)

Note that the full list of available parameters as well as their usage can be found on the [specification page](../aggregator-api-specification/evm-swaps.md).

For each of the token swaps queried, the `[V1] GET` API will return a data object consisting of:

* `routeSummary` ->  An object containing the routing data in human readable format. The API will only return the route with the best rate as determined by the KyberSwap Aggregator algorithm.
* `routerAddress` -> The address of the router contract which facilitates the swap

### Step 2: Encode Preferred Swap Route

Upon finding a favourable route, we can then go ahead and encode the selected route by including the `routeSummary` in the request body of [`[V1] Post Swap Route For Encoded Data`](../aggregator-api-specification/evm-swaps.md#chain-api-v1-route-build). Encoding the swap route via the API abstracts away the complexity of interacting with the contract directly.

```typescript
const requestBody = {
    routeSummary: routeSummary,
    sender: signerAddress,
    recipient: signerAddress,
    slippageTolerance: 10 //0.1%
}
```

[V1Post.ts](https://github.com/KyberNetwork/ks-aggregator-api-demo/blob/209a2d358fa3a47b50f87660c474d5592a155a13/src/apis/V1Post.ts#L21C1-L21C1)

Note that the `[V1] POST` API requires the `sender` and `recipient` to be appended to the `routeSummary` in order to configure the parties to the swap. In most cases, these would usually be the address that is executing the swap.

It is highly recommended that a `slippageTolerance` (in bips) is set to ensure that the swap proceeds smoothly within the boundaries set. Refer to [slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md) for more info regarding it's causes and effects on swap rates.

The encoded data for the selected swap route will be returned as a hexstring under the `data` object.

### Step 3: Execute Swap Transaction On-Chain

To execute the swap, we will leverage the [ethers.js](https://docs.ethers.org/v6/) library. For simplicity, we will hard code a private key under `/src/libs/signer.ts` that will allow us to programatically interact with the EVM from the backend.

With a configured signer, we can then execute the transaction on-chain by paying the necessary gas fees:

```typescript
const executeSwapTx = await signer.sendTransaction({
    data: encodedSwapData,
    from: signerAddress,
    to: routerContract,
    maxFeePerGas: 1000000000000,
    maxPriorityFeePerGas: 1000000000000        
});
```

[V1Swap.ts](https://github.com/KyberNetwork/ks-aggregator-api-demo/blob/209a2d358fa3a47b50f87660c474d5592a155a13/src/operations/V1Swap.ts#L28)

A tx hash will be returned once the swap tx has been successfully executed:

<figure><img src="../../../.gitbook/assets/Aggregator_DevGuide_SwapSuccess.png" alt=""><figcaption><p><a href="https://polygonscan.com/tx/0x149002bd7c5b290ecf31dc7d395cd3c0f97b19c1c8aeaf511541e9191dd29c7a">Sample swap on Polygon</a></p></figcaption></figure>
