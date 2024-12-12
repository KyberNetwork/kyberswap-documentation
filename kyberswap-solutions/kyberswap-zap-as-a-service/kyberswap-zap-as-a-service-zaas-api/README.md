---
description: >-
  Partners can directly integrate the API in their dapps. They will have to
  build their own front-end.
---

# KyberSwap Zap as a Service (ZaaS) API

## Zap In

The API consists of 2 main APIs - GetRoute and BuildRoute

* `GetRoute` is used to fetch the best zap route for adding liquidity to a new/existing position in a pool. It helps user preview the result of the zapping in action before confirming the transaction. The clients call this API once in a while, for example, to refresh the route preview displayed in the front-end client.
  * Request fields
    * The client is required to pass all the relevant fields
      * The dex to zap into
      * Pool's token 0, token 1 and fee tier
      * Position id or position lower and upper ticks (for UniswapV3-like dexes)
      * Input tokens and amounts
        * The tokens can be any ERC-20 token or `0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE` for the specific chain's native token (not limited to the pool's token0 or token1).
        * The amounts are full amounts without decimals (for example: `1000000` for `1 USDT`)
        * Slippage tolerance. This is used to calculate minimum swap output amount and minimum minted liquidity amount acceptable, otherwise the transaction will be reverted to protect against slippage.
      * Fee configuration: the client can opt to provide their fee collection address and fee per cent mille (0.001%) if they want to charge user with a fee
    * Provide a client id with the header `X-Client-ID` to get easier technical support and help facilitate better traffic observability.
      * By default, clients without a whitelisted client id are also rate limitted to 10 requests per 10 seconds. If you require a higher rate, please contact bd@kyber.network to request for a client id.
    * The client can optionally provide fee collection address and fee per cent mille (0.001%) to charge a fee from the input token. More details about zap's fee model can be found in the [Zap Fee Model](../zap-fee-model.md) page.
  * Response
    * Pool details
      * Include details about pool price before and after zapping in. Clients **should** use this data to provide their users with appropriate warnings, e.g. in case the pool price deviates too much from market price after zapping, which will subject the user's position to potential arbitrage
    * Position details
      * Give details about user new position after zapping. Please note that as usual, these details can get affected by slippage due to on-chain activities and the final result may differ slightly.
    * Zap details
      * Give details about how the zap is executed. For example it may or may not involves swapping with aggregator and/or swapping with the pool itself. It also includes details about fee amounts collected, remaining amounts left over after zapping, and the estimated price impact after zapping.
    * Route: this is the encoded zap route to be passed to `BuildRoute` if the user would like to execute it. The router address is used for clients to check for user allowance.
    * Gas information: this is an estimated value for the amount of gas needed for executing the transaction. Clients are advised to use from 2 to 2.5 times this amount as the max limit for sending the transaction to cater for fluctuation of the actual gas usage.
* `BuildRoute` is used to build the calldata from the route returned by GetRoute in order for the user to actually send the transaction on-chain. The clients call this API once the user confirm they want to execute the zap-in, then use the calldata and other details in the response to send the transaction on chain.
  * This endpoint simply returns the needed call data, transaction value, and router address to send the transaction to.



## Zap Migrate

Similar to Zap In, Zap Migrate API consists of 2 main APIs - GetRoute and BuildRoute

Please refer to the two API specifications below for details about request and response fields.



<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td>ZaaS HTTP API</td><td></td><td><a href="zaas-http-api.md">zaas-http-api.md</a></td></tr><tr><td></td><td>ZaaS GRPC API</td><td></td><td><a href="zaas-grpc-api.md">zaas-grpc-api.md</a></td></tr></tbody></table>
