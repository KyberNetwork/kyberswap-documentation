---
description: Trustless On-Chain Price And Liquidity Data
---

# TWAP Oracle

## Introduction

KyberSwap Elastic now exposes an [oracle](../../../getting-started/foundational-topics/decentralized-technologies/oracles.md) service which enables historical price data to be queried [on-chain](../../../getting-started/foundational-topics/decentralized-technologies/on-chain-vs-off-chain-data.md) directly from the pool contracts. This significantly expands the range of potential on-chain use cases which require trustless access to the latest pool pricing data. With KyberSwap Elastic TWAP (time weighted average price) oracles, anyone connected to the blockchain will be able to build on top of Elastic pool's historical price feed.

## Geometric mean TWAP

To minimize the risks of oracle manipulation as well as ensure price feed accuracy and reliability, KyberSwap Elastic maintains an array of [tick](tick-range-mechanism.md) observations from which the geometric mean time-weighted average price (TWAP) can be computed. Note that the geometric mean is much less susceptible to data outlier points hence is a better measure of the true "average" of price observations.&#x20;

The geometric mean TWAP is a crucial piece of the oracle design as it not only smoothens out the market volatility but also significantly increases the cost of any back-running attacks. By swapping a significant amount of an asset, the attacker can cause the pool price to cross multiple ticks within a single block. The oracle will then be updated based on the final pool price when the block was mined. The attacker can then conduct a swap of the same magnitude in the opposite direction in the next block to recover their initial capital. The risk for a back-run attack exists as long as the potential profit outweighs the transaction costs of these 2 swaps.

The potential profit for an attack arises from downstream on-chain services that leverages the oracle price feed for their own services. This could range from more basic services such as collateralized loans or more complex financial products such as derivative contracts. With the geometric mean TWAP mechanism, the financial capital required to pull-off an attack that results in a substantial oracle price change becomes prohibitively expensive relative to the expected payout. Moreover, such services can cheaply defend against such manipulations by querying multiple historical price observations given that the price manipulation will only affect the latest observations.

## Implementation overview

### Observations

Historical pricing data is stored as an array of observations with each observation consisting of the following data (view the contract library [here](https://github.com/KyberNetwork/ks-elastic-sc/blob/main/contracts/libraries/Oracle.sol)):

```solidity
  struct Observation {
    // the block timestamp of the observation
    uint32 blockTimestamp;
    // the tick accumulator, i.e. tick * time elapsed since the pool was first initialized
    int56 tickCumulative;
    // whether or not the observation is initialized
    bool initialized;
  }
```

An `observation` is a snapshot of the time weighted tick at the last block where the tick was active (i.e. active price crosses into a neighbouring tick in the next block). The first `observation` is initialized together with the oracle, which is usually at the point of pool creation. The existing `observation` is either overwritten or a new `observation` entry is added to the array whenever a tick is crossed.

### Tick accumulator

The `tickCumulative` stores the time weighted sum of the tick at the time of the observation. For every block whereby the tick supports the active price, the `tickCumulative` is incremented by the relevant tick value multiplied by the time elapsed since pool creation. The `tickCumulative` therefore indirectly maintains the total amount of time that the observed tick has supported the market price.

To support the geometric mean TWAP, KyberSwap Elastic pool oracle keeps track of the accumulated arithmetic sum of the current ticks to the timestamp $$t$$:

$$
a_t = \sum_{i=t_0}^t tick_i\approx \sum_{i=t_0}^t log_{1.0001}p_i
$$

In order to derive the approximated geometric TWAP between a time interval $$(t_1, t_2)$$, we can use the following formula:

$$
\begin{align*}
p_{(t_1, t_2)}&=(\prod_{i=t_1}^{t_2} p_i)^\frac{1}{t_2-t_1} \\
&=(\prod_{i=t_1}^{t_2} 1.0001^{log_{1.0001} p_i})^\frac{1}{t_2-t_1} \\
&\approx 1.0001^{{\sum_{i=t_1}^{t_2}tick_i}\frac{1}{t_2-t_1}} \\
&= 1.0001^{\frac{a_{t_2}-a_{t_1}}{t_2-t_1}}
\end{align*}
$$

### Cardinality

In addition to the `tickCumulative`, KyberSwap Elastic oracle also keeps track of additional `ObservationData` (view contract [here](https://github.com/KyberNetwork/ks-elastic-sc/blob/main/contracts/oracle/PoolOracle.sol)):

```solidity
  struct ObservationData {
    bool initialized;
    // the most-recently updated index of the observations array
    uint16 index;
    // the current maximum number of observations that are being stored
    uint16 cardinality;
    // the next maximum number of observations to store, triggered in observations.write
    uint16 cardinalityNext;
  }
```

The `cardinality` is a measure of observation slots that have been initialized while `cardinalityNext` indicates the number of available slots. By utilizing the above two variables, users can conveniently check the number of available observation slots as well as increase the number of available observation slots if more observations are required.

Note that both `cardinality` and `cardinalityNext` are of type `uint16` meaning that the oracle only enables a maximum of `(2^16)-1` observation slots which equates to `65,536` observation slots. For Ethereum mainnet which has an [average block time of 12s](https://etherscan.io/chart/blocktime), this is equivalent to having a new tick initialized every consecutive block and therefore a new observation being created and tracked for a minimum of \~9 days. The observation array is designed to overflow with the newest observations replacing the oldest observations.
