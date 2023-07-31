---
description: Interacting With KyberSwap Aggregator Router Contract
---

# Execute A Swap With The Aggregator API

## Overview

KyberSwap maintains a single API specification for all EVM chains:

* [Swap API specs for EVM chains](../aggregator-api-specification/evm-swaps.md)

{% hint style="info" %}
#### KyberSwap Aggregator APIv2

Following feedback on the initial non-versioned API, KyberSwap has implemented a more performant `[V1]` API which improves the response time for getting a route via offloading encoding requirements to the post method.

For integrators who have previously integrated with the non-versioned API, please refer to [Upgrading To APIv1](upgrading-to-apiv1.md) for further details on the motivation behind the upgrade as well as the relevant changes to swap flow and parameters.&#x20;

Please use the `[V1]GET` API for more efficient route queries. The returned route can then be reused in the `[V1]POST` body to get the encoded swap data. The non-versioned`GET` and `[V1]GET` remains backwards compatible with the main change being the queried path.&#x20;

**While both versions of the API remains backwards compatible, only the `[V1]` APIs will continue to receive updates and hence developers are highly encouraged to implement the latest `[V1]` APIs to avoid any disruptions as the non-versioned API is eventually deprecated.**
{% endhint %}

## Sequence diagram

<figure><img src="../../../.gitbook/assets/Aggregator APIv2-APIv2.png" alt=""><figcaption><p>APIv2 sequence diagram</p></figcaption></figure>

To execute a swap, the router (`MetaAggregationRouterV2`) contract requires the encoded swap data to be included as part of the transaction. This encoded swap data as well as other swap metadata are returned as part of the API response. As such, developers are expected to call the swap API prior to sending a transaction to the router contract.

## Web3.js example

### Swap Params Response[​](https://docs.kyberswap.com/Aggregator/implement-a-swap#swap-params-response) <a href="#swap-params-response" id="swap-params-response"></a>

| Parameter Name  | Type   | Required | Description                            |
| --------------- | ------ | -------- | -------------------------------------- |
| inputAmount     | string |          | hex string represents the input amount |
| routerAddress   | string |          | ERC20 contract address of the router   |
| encodedSwapData | string |          | hex data to be used in transaction     |
| ...             |        |          |                                        |

{% hint style="info" %}
The response parameters have been slightly altered in the `[V1]POST` API. The relevant parameter keys are provided below ( non-versioned -> `[V1]`):

* `inputAmount` -> `amountIn`
* `encodedSwapData` -> `data`
{% endhint %}

The Encoded Swap API response includes `inputAmount` and `encodedSwapData` above to be used as data to interact with our smart contract. By using the `encodedSwapData`, you don't have to care about the logic behind the encoding process. The next section will explain client usage

### Web3js Client Integration[​](https://docs.kyberswap.com/Aggregator/implement-a-swap#web3js-client-integration) <a href="#web3js-client-integration" id="web3js-client-integration"></a>

Web3.js integration is relatively straightforward but to avoid transaction failure due to gas, we recommend performing a gas estimation call.

#### Initial web3 context[​](https://docs.kyberswap.com/Aggregator/implement-a-swap#initial-web3-context) <a href="#initial-web3-context" id="initial-web3-context"></a>

```javascript
const { account, chainId, library } = useActiveWeb3React()
```

#### Estimate gas[​](https://docs.kyberswap.com/Aggregator/implement-a-swap#estimate-gas) <a href="#estimate-gas" id="estimate-gas"></a>

_Note: The value of the transaction is the `inputAmount` if the input token is a native token, and 0 otherwise_

```javascript
const amountIn = tokenIn == ETHER ? response.InputAmount : 0

const estimateGasOption = {
        from: account,
        to: trade.routerAddress,
        data: trade.encodedSwapData,
        value: BigNumber.from(amountIn),
      }
      
const gasEstimate = await library
        .getSigner()
        .estimateGas(estimateGasOption)
        .then(response => {
          return response
        })
```

#### Execute transaction call[​](https://docs.kyberswap.com/Aggregator/implement-a-swap#execute-transaction-call) <a href="#execute-transaction-call" id="execute-transaction-call"></a>

Using the `gasEstimate` function above to combine with the transaction object

_Note: The value of the transaction is the `inputAmount` if the input token is a native token, and 0 otherwise_

```javascript
const amountIn = tokenIn == ETHER ? response.InputAmount : 0

const sendTransactionOption = {
    from: account,
    to: api.routerAddress,
    data: api.encodedSwapData,
    gasLimit: gasEstimate,
    gasPrice: gasPrice,
    ...(trade.inputAmount.currency instanceof Token
          ? {}
          : { value: BigNumber.from(inputAmount) }),
}

library
    .getSigner()
    .sendTransaction(sendTransactionOption)
```
