---
description: Query Historical Price Data
---

# Get Elastic Pool Price

## Overview

KyberSwap Elastic enables integrators to trustlessly query the time-weighted average price of an Elastic pool via the [`poolOracle`](https://github.com/KyberNetwork/ks-elastic-sc/blob/main/contracts/oracle/PoolOracle.sol) contract. Integrators can then derive the geometric mean to get an accurate representation of the pool's price data. For more information on the variable definitions, concepts, and implementation details, please refer to [TWAP Oracle](../concepts/twap-oracle.md).

{% hint style="success" %}
**Elastic SDK**

KyberSwap has created an [Elastic SDK](https://github.com/KyberNetwork/ks-sdk-elastic) to make interacting with our Elastic smart contracts easier. You can refer to our [Elastic SDK Developer Guides](../../elastic-sdk/developer-guides/) for step-by-step walkthroughs on how to achieve various Elastic operations in a TypeScript environment.
{% endhint %}

## Getting the pool price

### Retrieve the accumulated tick

To compute the TWAP, we first need to retrieve the [tick accumulator](../concepts/twap-oracle.md#tick-accumulator) for the requested time period. The `poolOracle` contract exposes an [`observeFromPool()`](https://github.com/KyberNetwork/ks-elastic-sc/blob/main/contracts/oracle/PoolOracle.sol#L136) function which expects:

* `pool`: The address of the pool whose price is being queried
* `secondsAgo`: A list of the amount of time, in seconds, since the query at which to return the [`tickCumulative`](../concepts/twap-oracle.md#tick-accumulator) value.

Note that a `secondsAgo` value of `0` or a value later than the last [observation](../concepts/twap-oracle.md#observations) will return the latest `tickCumulative` value. If the target time matches an observation timestamp, the corresponding `tickCumulative` of the observation will be returned. If the target time is between two observations, the interpolated `tickCumulative` of the two observations will be returned.

### Calculating the geometric mean TWAP

Following the query above, we can then extract the average price by using this formula:

$$
\begin{align*}
p_{(t_1, t_2)}&=(\prod_{i=t_1}^{t_2} p_i)^\frac{1}{t_2-t_1} \\
&=(\prod_{i=t_1}^{t_2} 1.0001^{log_{1.0001} p_i})^\frac{1}{t_2-t_1} \\
&\approx 1.0001^{{\sum_{i=t_1}^{t_2}tick_i}\frac{1}{t_2-t_1}} \\
&= 1.0001^{\frac{a_{t_2}-a_{t_1}}{t_2-t_1}}
\end{align*}
$$

#### Assumptions

* We are querying a `WETH/USDT` pool to get the average price for the pool over the last hour
* Using a `secondsAgo` of `[0, 3600]`, the `observeFromPool()` function above returns a `tickCumulatives` value of `[500000000, 225000000]`.

#### Calculation

Plugging in the values, we get:

$$
p_{(t_1, t_2)}= 1.0001^{\frac{a_{t_2}-a_{t_1}}{t_2-t_1}}
$$

$$
p_{(t_1, t_2)}= 1.0001^{\frac{500,000,000-225,000,000}{3,600-0}}=1.0001^{76,389}=2,076.66 \text{USDC/WETH}
$$
