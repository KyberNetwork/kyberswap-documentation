---
description: Uncover The Best Pools
---

# Get Elastic Pool Addresses

## Overview[​](https://docs.kyberswap.com/Classic/contract/fetching-pool-addresses#overview) <a href="#overview" id="overview"></a>

For each token pair, there are possibly many multiple pools with different configurations. As such, it is necessary to specify which pools are to be used for fetching token rates, trade execution and liquidity provision.

{% hint style="success" %}
**Elastic SDK**

KyberSwap has created an [Elastic SDK](https://github.com/KyberNetwork/ks-sdk-elastic) to make interacting with our Elastic smart contracts easier. You can refer to our [Elastic SDK Developer Guides](../../elastic-sdk/developer-guides/) for step-by-step walkthroughs on how to achieve various Elastic operations in a TypeScript environment.
{% endhint %}

## Selecting the right pool

KyberSwap Elastic contract provides a function to get a specific pool. For each inputs including `tokenIn`, `tokenOut`, `fee` there will be an exact pool.

The input fee parameter can be:

* `8` in BPS \~ 0.008%
* `10`in BPS \~ 0.01%
* `40`in BPS \~ 0.04%
* `300`in BPS \~ 0.3%
* `1000`in BPS \~ 1%

### `getPool()`[​](https://docs.kyberswap.com/contract/get-pool#getpool) <a href="#getpool" id="getpool"></a>

Returns the pool address for a given pair of tokens and a swap fee. Note that the token order does not matter.

**Input**[**​**](https://docs.kyberswap.com/contract/get-pool#input)

| Field        | Type      | Explanation                                 |
| ------------ | --------- | ------------------------------------------- |
| `tokenA`     | `address` | contract address of either token0 or token1 |
| `tokenB`     | `address` | contract address of the other token         |
| `swapFeeBps` | `uint16`  | swap fee, in basis points                   |

**Output**[**​**](https://docs.kyberswap.com/contract/get-pool#output)

| Field  | Type      | Explanation                                                 |
| ------ | --------- | ----------------------------------------------------------- |
| `pool` | `address` | The pool address. Returns null address if it does not exist |
