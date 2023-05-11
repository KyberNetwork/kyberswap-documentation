---
description: Understanding Your Elastic APR
---

# Elastic APR Calculations

{% hint style="info" %}
#### KyberSwap APRs

As each liquidity position in Elastic is non-fungible, different formulas are required in order to provide users with a best estimate of the expected returns. To this end, KyberSwap computes the following APRs for Elastic LPs:

* [**Elastic Pool APR**](apr-calculations.md#annual-percentage-rate-apr-calculation): The APR for the pool. Calculated by sampling the fees over the active liquidity range every 30 minutes for the last 24 hours and extrapolates to an annual basis.
* [**My Pool APR**](apr-calculations.md#my-pool-apr-calculation): The APR for a specific position within a pool. My Pool APR is calculated by extrapolating the total fees earned since the position was created over the period of a year.
* [**My Farm APR**](apr-calculations.md#my-farm-apr-calculation): The APR for all positions within a specific farm. My Farm APR is calculated by dividing the 24H farm rewards over the USD value of the position and extrapolating it over a period of a year.
{% endhint %}

## Elastic Pool Annual Percentage Rate (APR) calculation[​](https://docs.kyberswap.com/overview/elastic-pool-apr-calculation#annual-percentage-rate-apr-calculation) <a href="#annual-percentage-rate-apr-calculation" id="annual-percentage-rate-apr-calculation"></a>

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

### Example Elastic pool APR calculation[​](https://docs.kyberswap.com/overview/elastic-pool-apr-calculation#example-apr-calculation) <a href="#example-apr-calculation" id="example-apr-calculation"></a>

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
| 1                  | 1128 - 1200 | 1000      | <mark style="color:green;">Yes</mark> |
| 2                  | 1164 - 1236 | 3000      | <mark style="color:green;">Yes</mark> |
| 3                  | 1178 - 1212 | 5000      | <mark style="color:green;">Yes</mark> |
| 4                  | 1212 - 1272 | 2000      | <mark style="color:red;">No</mark>    |

* Return for the interval (12:00 PM, 3rd Jan ←→ 12:30 PM, 3rd Jan) = (2000/9000) \* 100% = 0.00222%

The above calculation is repeated for each of the 48 intervals with the total returns for the day being the sum of all 48 intervals. This is then multiplied by 365 days to get the final estimated APR. For simplicity, assuming all 48 intervals have the exact same fees and TVL, the APR would be 38.93% (0.00222% \* 48 \* 365 ).

## My Pool APR calculation

As each Elastic position supports [specific liquidity ranges](concentrated-liquidity.md), the APR of a position varies greatly depending on whether the position is in-range (i.e. supporting the currently active trading price)  or out-of-range (i.e. outside the active trading price). Trading fees are only distributed to positions which have supported the trade and hence the My Pool APR calculations have to consider the customized liquidity range that was selected by the user.

To account for the unique price ranges for each position, the My Pool APR calculation aggregates the trading fees that was earned by the position since its creation and extrapolates it over 365 days. In doing so, KyberSwap is able to provide a more accurate My Pool APR as the historical fees generated by that position already comprises the status of the position (i.e. in-range or out-of-range). As a result, the My Pool APR tends to smoothen out over a longer time period as variances caused by short-term market fluctuations will be distributed more evenly.

### Example My Pool APR calculation

#### Scenario

A user opens a new position in the `ETH - USDT (1% fee tier)` Elastic Pool with a dollar value of USD1000. Over the course of 30 days, the `ETH` price swings significantly and his position constantly goes in and out of range. After 30 days, the position accumulates USD50 in fees.

#### Calculation

To calculate the My Pool APR, we assume that the position will continue to earn fees at a similar rate to the last 30 days. As such, extrapolating this to 365 days, the position is expected to earn \~USD608.33 (50/30 \* 365) over the course of the year.

To get the My Pool APR, we take the expected annual earnings and divide it by the position's value:

$$
MyPoolAPR = \frac{EstimatedAnnualEarnings}{PositionCurrentValue}* 100\%
$$

$$
MyPoolAPR = \frac{608.33}{1000}*100\%=60.83\%
$$

## Elastic farm APR calculation

As Elastic farm rewards are based on the [active time of liquidity](tick-based-farming.md#farming-mechanisms), the expected APR will be directly proportional to the amount of time which the user's underlying liquidity goes into supporting the active price. Given that this is highly dependent on the position's range which the LP has set relative to the market price, the estimated APRs for Elastic farm are computed using the TVL of the underlying pool (both in and out of range positions). As such, **the Elastic farm APRs displayed are the minimum returns that a staker can expect to receive by participating in the pool.**&#x20;

As long as the staked position supports the active price range, returns will always exceed the stated Elastic farm APRs. The more [concentrated](concentrated-liquidity.md) the liquidity supporting the market price, the more rewards distributed to the position. Note that positions outside the active range are not eligible for farming rewards. The Elastic farm APR formula below simplifies the APR calculations so as not to add on the complexity of dynamically accounting for market movements as well as customized liquidity ranges which can go in and out of range.

$$
FarmAPR=\frac{TotalFarmRewards}{TVL_{underlyingPool}}*\frac{365 \text{ days}}{Time_{totalFarm}}*100\%
$$

Note that the total farm rewards are spread across the full TVL of the underlying pool. Consequently, any position that is staked and supporting the active price will receive a higher APR due to the fact that the position's liquidity will be more concentrated than the pool's min and max range.

### Example Elastic farm APR calculation

#### Scenario

A farm is setup to distribute 100,000`USDT` as farming rewards for the  `ETH - USDT (1% fee tier)` Elastic Pool over the duration of 14 days. Upon the farm being launched, multiple LPs stake a total of USD300,000 to benefit from the farming rewards.

#### Calculation

For simplicity, farming rewards are distributed in `USDT` and it is assumed that `USDT` maintains it's peg with the US dollar. Note that the APR calculation is based on the USD value of the rewards and TVL. To get the farm APR, we just need to plug the values above into the formula.

$$
FarmAPR=\frac{TotalFarmRewards}{TVL_{underlyingPool}}*\frac{365 \text{ days}}{Time_{totalFarm}}*100\%
$$

$$
FarmAPR=\frac{100,000}{300,000}*\frac{365}{14}*100\%=8.69\%
$$

## My Farm APR calculation

In a similar fashion to the My Pool APR, the My Farm APR can be obtained by extrapolating the rewards received by a staked position over the period of a year. Farming rewards are only distributed to positions which have supported the trade and hence the My Pool APR calculations have to consider the customized liquidity range that was selected by the user.

To account for the unique price ranges for each position, the My Farm APR calculation aggregates the rewards that was earned by the position over the last 24 hours and extrapolates it over 365 days. In doing so, KyberSwap is able to provide a more accurate My Farm APR as the historical rewards earned by that position already comprises the status of the position (i.e. is it in-range or out-of-range).&#x20;

In the case of My Farm APR, the rewards streamed per day is constant and known at the time of farm setup. As such, the My Farm APR will be determined by the amount of time that a staked position is in range as well as the current value of the position.



$$
MyFarmRewards_{24H}=\frac{UserInRangeStakedTVL_{24H}}{FarmInRangeStakedTVL_{24H}}*FarmRewards_{24H}
$$

The expected My Farm APR can then be extrapolated based on the daily rewards allocated to the staked position:

$$
MyFarmAPR=\frac{MyFarmRewards_{24H}}{CurrentValue_{position}}*365days*100\%
$$

In this case, the value of the rewards allocated to the user is compared against the value of the underlying position. This allows stakers to estimate their farming returns based on the liquidity that their stake has contributed to the supporting the farm's active ranges.

### Example My Farm APR calculation

As an example, to calculate the farm APR for a staked position, we first get the total rewards that the position accrues in a day. For simplicity, assume that our sample position of USD10,000 accrues 10USD a day, we will get the following APR:

$$
MyFarmAPR=\frac{MyFarmRewards_{24H}}{CurrentValue_{position}}*365days*100\%
$$

$$
MyFarmAPR=\frac{10*365}{10,000}*100\%=36.5\%
$$
