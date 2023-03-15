---
description: Fees That React To Market Conditions
---

# Dynamic Auto-Adjusting Fees

## Introduction

KyberSwap Classic introduces a dynamic LP fee model which adjusts according to market volatility as measured by the on-chain volume of each pool. In contrast to the static fees found in most AMM implementation, KyberSwap Classic provides the option to automatically decrease trading fees in periods of low volatility to incentivize more trading and vice versa. Put more conventionally, KyberSwap Classic is able to automatically adjust the trading spread according to market conditions. This more accurately reflects the prevailing market making spread and encourages greater market stability.&#x20;

Critically, this flexibility provides greater impermanent loss protection as fees scale with the potential pool impermanent loss. Lower fees during periods of relative calm encourages more trades which would potentially lead to higher returns if the incremental trade volume offsets the reduced fees. On the other hand, higher fees during periods of relative volatility acts as an impermanent loss premium due to the increased risk LPs face during such periods.&#x20;

## Dynamic fee adjustment based on volume <a href="#dynamic-fee-adjustment-based-on-volume" id="dynamic-fee-adjustment-based-on-volume"></a>

There are several ways to implement this dynamic fee adjustment mechanism deterministically. KyberSwap's approach is based on the on-chain volume of each pool. To determine the fluctuation of KyberSwap's volume, the AMM compares its volume between the short window and long window using methodologies such as Simple Moving Average (SMA) or Exponential Moving Average (EMA).

Based on this bonding function, when users want to sell $$Δx$$, the formula for $$Δy$$ they get in the Dynamic Fee model is:

$$
\Delta y = f(x) - f(x + \Delta x \cdot (1 - fee - z))
$$

where:

* $$x,y$$ are the current inventories of 2 assets $$X,Y$$
* $$fee$$ is the base fee, pre-defined by AMM
*   $$z$$ is the variant factor, dependent on the average volume of AMM during a time period. It must satisfy the condition $$0<1−fee-z≤1$$, alternatively written as $$−fee≤z<1−fee$$



## Price correlation and fee ranges

KyberSwap Classic's dynamic fee movement is bounded by a fee range which is informed by the relative price stability between the token pairs. KyberSwap Classic has implemented the following fee ranges based on our market observations:

| Asset Pairs Price Stability | Amplification Factor | Fee Range (bps) |
| --------------------------- | -------------------- | --------------- |
| Similar                     | 20 < AMP             | 2 - 8           |
| Strongly Correlated         | 5 < AMP ≤ 20         | 5 - 20          |
| Correlated                  | 2 < AMP ≤ 5          | 10 - 40         |
| Weakly Correlated           | 1 ≤ AMP ≤ 2          | 15 - 60         |
