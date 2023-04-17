---
description: Understanding Your Elastic APR
---

# Elastic Pool APR Calculations

## Annual Percentage Rate (APR) calculation[​](https://docs.kyberswap.com/overview/elastic-pool-apr-calculation#annual-percentage-rate-apr-calculation) <a href="#annual-percentage-rate-apr-calculation" id="annual-percentage-rate-apr-calculation"></a>

To demonstrate the practicality of the [reinvestment curve design](https://docs.kyberswap.com/overview/elastic-walkthrough), KyberSwap also displays an average APR for each Elastic pool. In order to provide a more accurate estimate of potential APR, the average APR calculation will have to prioritize active liquidity positions which were accumulating fees during a selected time interval. As such, APR calculations are based on the historical data for the selected pool. KyberSwap Elastic APR calculations are based on 30 minute intervals whereby the return per interval is:

$$
\frac{PoolFees}{TVL_{InRange} } * 100\%
$$

Extending this over a day, we get the sum for 48 intervals (30 min each). This is the daily return if your liquidity position was in range for the whole day:

$$
\sum_{0<x\le 48}(\frac{PoolFees}{TVL_{ InRange}}) * 100\%
$$

To get the APR from the last 24 hours of trading data, we multiply the above by the number of days in a year. The final APR calculation is as follows:

$$
\sum_{0<x\le 48}(\frac{PoolFees}{TVL_{ InRange}}) * 100\% * 365
$$

{% hint style="info" %}
#### Data sampling and APR accuracy

To account for market volatility which could result in significant changes to the pool's liquidity within the specified 30 minute interval, the APR formula samples the data according to the following rules:

* $$PoolFees$$ is calculated at the end of the interval to account for all fees earned over the interval period
* $$TVL_{InRange}$$ is calculated at the beginning of the interval to determine positions which have supported the pool in the past

By sampling 48 times throughout a day, the APR displayed better approximates the expected APR for the pool as intraday variances are smoothened out.
{% endhint %}

### Example APR calculation[​](https://docs.kyberswap.com/overview/elastic-pool-apr-calculation#example-apr-calculation) <a href="#example-apr-calculation" id="example-apr-calculation"></a>

#### Scenario[​](https://docs.kyberswap.com/overview/elastic-pool-apr-calculation#scenario) <a href="#scenario" id="scenario"></a>

A user holding some `ETH` and `USDT` is planning to earn yield for her asset by contributing liquidity to a KyberSwap Elastic Pool. She visits the [Elastic Pools page](https://kyberswap.com/pools/) at 10:00 AM, 4th Jan to view the available pools and notices that the `ETH - USDT (1% fee tier)` Elastic Pool offers the highest APRs. Before committing her tokens, she would like to understand how this APR is calculated.

#### Assumptions[​](https://docs.kyberswap.com/overview/elastic-pool-apr-calculation#assumptions) <a href="#assumptions" id="assumptions"></a>

* APR is being calculated for the `ETH - USDT (1% fee tier)` Elastic Pool at 10:00AM, 4th Jan
* The current price of the pool is 1200
* Based on the current price, the [tick ranges](https://docs.kyberswap.com/overview/elastic-walkthrough) of the pool increases in roughly 1% (\~12USD) steps:

<figure><img src="../../../.gitbook/assets/APR Calculation-Ticks.drawio.png" alt=""><figcaption><p>Ticks</p></figcaption></figure>

#### Single interval calculation[​](https://docs.kyberswap.com/overview/elastic-pool-apr-calculation#single-interval-calculation) <a href="#single-interval-calculation" id="single-interval-calculation"></a>

To calculate the return for the earliest time interval (10:00 AM, 3rd Jan ←→ 10:30 AM, 3rd Jan):

* 30m Fees at the end of the interval = USD2000
* Pool price at the end of the interval (12 PM, 3rd Jan ←→ 12:30 PM, 3rd Jan). This is used to calculate in-range positions for this interval = 1190
* Based on above price, the 30m tick range to consider = 1188-1200 (.....1176 - **1188 - 1200** - 1212.....)

<figure><img src="../../../.gitbook/assets/APR Calculation-TVL.drawio (4).png" alt=""><figcaption><p>Position TVL</p></figcaption></figure>

* TVL for active liquidity positions that supported the tick 1188-1200 at 12PM, 3rd Jan = USD9000 (aggregate TVL of position 1 + 2 + 3 below)

| Liquidity Position | Tick Range  | TVL (USD) | Included                              |
| ------------------ | ----------- | --------- | ------------------------------------- |
| 1                  | 1100 - 1200 | 1000      | <mark style="color:green;">Yes</mark> |
| 2                  | 1152 - 1212 | 500       | <mark style="color:green;">Yes</mark> |
| 3                  | 1188 - 1236 | 250       | <mark style="color:green;">Yes</mark> |
| 4                  | 1100 - 1188 | 500       | <mark style="color:red;">No</mark>    |

* Return for the interval (12:00 PM, 3rd Jan ←→ 12:30 PM, 3rd Jan) = (2000/9000) \* 100% = 0.00222%

The above calculation is repeated for each of the 48 intervals with the total returns for the day being the sum of all 48 intervals. This is then multiplied by 365 days to get the final estimated APR. For simplicity, assuming all 48 intervals have the exact same fees and TVL, the APR would be 38.93% (0.00222% \* 48 \* 365 ).
