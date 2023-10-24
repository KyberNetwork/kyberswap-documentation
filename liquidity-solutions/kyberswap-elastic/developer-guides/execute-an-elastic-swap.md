---
description: Trade Directly Against An Elastic Pool
---

# Execute An Elastic Swap

## Obtaining pool addresses

It is necessary to specify which pools are to be used for the token swap. Read more about [fetching pool addresses](get-elastic-pool-addresses.md) before proceeding.

{% hint style="success" %}
**Elastic SDK**

KyberSwap has created an [Elastic SDK](https://github.com/KyberNetwork/ks-sdk-elastic) to make interacting with our Elastic smart contracts easier. You can refer to our [Elastic SDK Developer Guides](../../elastic-sdk/developer-guides/) for step-by-step walkthroughs on how to achieve various Elastic operations in a TypeScript environment.
{% endhint %}

## Executing a swap

After getting a pool address from [getPool()](https://docs.kyberswap.com/integration/contract/get-pool), you can call `swap()` function to execute a swap.

### `swap()`[​](https://docs.kyberswap.com/contract/implement-a-swap#swap) <a href="#swap" id="swap"></a>

Swap token0 -> token1, or vice versa. Note that swaps will either fully use up the specified swap quantity, or swap up to the specified price limit, depending on whichever condition is satisfied first.

#### **Input**[**​**](https://docs.kyberswap.com/contract/implement-a-swap#input)

| Field        | Type      | Explanation                                                                                   |
| ------------ | --------- | --------------------------------------------------------------------------------------------- |
| `recipient`  | `address` | address to receive the swap output                                                            |
| `swapQty`    | `int256`  | swap quantity, which implicitly configures the swap as exact input (>0), or exact output (<0) |
| `isToken0`   | `bool`    | whether the swapQty is specified in token0 (true) or token1 (false)                           |
| `limitSqrtP` | `uint160` | sqrt price limit to reach                                                                     |
| `data`       | `bytes`   | Data, if any, to be passed into the callback function                                         |

#### **Note**[**​**](https://docs.kyberswap.com/contract/implement-a-swap#note)

To specify an unlimited price limit for a swap, use the following values.

| `isToken0` | `swapQty` | Value                |
| ---------- | --------- | -------------------- |
| `true`     | > 0       | `MIN_SQRT_RATIO + 1` |
| `true`     | < 0       | `MAX_SQRT_RATIO - 1` |
| `false`    | > 0       | `MAX_SQRT_RATIO - 1` |
| `false`    | < 0       | `MIN_SQRT_RATIO + 1` |

#### **Output**[**​**](https://docs.kyberswap.com/contract/implement-a-swap#output)

| Field  | Type     | Explanation                                                                   |
| ------ | -------- | ----------------------------------------------------------------------------- |
| `qty0` | `int256` | exact token0 qty sent to recipient if < 0. Minimally received quantity if > 0 |
| `qty1` | `int256` | exact token1 qty sent to recipient if < 0. Minimally received quantity if > 0 |
