---
description: Auto-Compounding LP Fees
---

# Reinvestment Curve

## Introduction

As [concentrated liquidity](concentrated-liquidity.md) AMMs grew in popularity with the explosion of DeFi summer, its key limitation became increasingly apparent: LP fees sat in the contract unutilized and required significant gas fees to be collected and reinvested. For most, the opportunity cost of idle LP fees was a price which they were willing to pay given the significantly better yields which concentrated liquidity positions offered (as there were limited alternatives). Nevertheless, the gas costs required to constantly reinvest LP fees could quickly become prohibitively expensive for all except the largest LPs. This is also not taking into account the administrative overhead required to manually reinvest LP fees.

The reinvestment curve was a novel solution that was launched with KyberSwap Elastic. The reinvestment curve was designed with the sole purpose of natively reinvesting otherwise unutilized LP fees in the concentrated liquidity model. This meant LP fees for concentrated liquidity positions were automatically compounded without the gas nor the manual management overhead. Moreover,  LPs still have the option to collect their auto-compounded fee earnings separately at any point in time.&#x20;

Crucially, the auto-compounding of yields meant that any LP fees were immediately reinvested therefore ensuring even greater capital efficiency. As such, the reinvestment curve enables otherwise idle capital (i.e. earned interest) to earn an incremental amount of the fees.

## Implementation overview

To achieve this feat of auto-compounding yields for non-fungible liquidity positions, KyberSwap Elastic introduced the reinvestment curve which is an additional AMM pool where fees received from the original pool would accrue to. As LP fees are added to the pool, new reinvestment curve liquidity tokens are minted for the original liquidity position. Through aggregating the reinvestment curve with the original price curve, KyberSwap Elastic enables LP fees to be compounded even when a position goes out of range. Put more formally, LP fees are reinvested into the pool at an infinite range.

## Technical explanation

### Compounding fee[​](https://docs.kyberswap.com/overview/elastic-walkthrough#compounding-fee) <a href="#compounding-fee" id="compounding-fee"></a>

In Uniswap v3, the fees are taken in the form of token0 & token1 separately, which do not contribute to the pool's liquidity. This limit makes Uniswap v3 not directly compoundable within the protocol. The KyberSwap Elastic protocol inherits the liquidity concentration of KyberSwap Classic and achieves customizability of Uniswap v3 while preserving the compounding feature. This is achieved by placing collected fees into a reinvestment curve, which is aggregated with the pool.

The reinvestment curve is a compoundable constant product curve that supports the price range from 0 to infinity. The reinvestment curve is aggregated with the pool so that both pools maintain a common price while behaving differently. Price ranges of the pool have different amounts of liquidity, which are not affected by exchange activities. Meanwhile, the reinvestment curve's liquidity remains the same on all ticks and increases based on the accumulating fee after each swap.

### Reinvestment curve[​](https://docs.kyberswap.com/overview/elastic-walkthrough#reinvestment-curve) <a href="#reinvestment-curve" id="reinvestment-curve"></a>

Assume that:

* $$x,y$$: reserve of token in/out
* $$Δx,Δy$$: amount in/out
* $$L$$: liquidity

Base formula:

**(1.1)** $$x*y=L^2$$

Currently, the trade fee will be calculated as a proportion of amountIn = ($$\Delta x * fee$$). This amount will be reinvested into the pool as an addition of liquidity:&#x20;

**(1.2)** $$(x + \Delta x * fee) * y = (L + \Delta L)^2$$

This can be approximated to&#x20;

**(1.3)** $$\Delta L =\Large \frac{L * fee * \Delta x}{2 * x}$$&#x20;

with the assumption that

**(1.4)** $$\Delta x * fee << x$$

the equation after swap:&#x20;

**(1.5)** $$(x + \Delta x) * (y - \Delta y) = (L + \Delta L)^2$$&#x20;

By **(1.3)**, we calculate the incremental liquidity based on the amount in and fee; and then by **(1.5)** we calculate the amount out based on the amount in and incremental liquidity.

After the swap, the constant product curve in 1.1 remains unchanged except that a small proportion of liquidity is added into the curve in the form of reinvestment liquidity. The pool contract will needs to keep track of 2 variables: `baseL` is the liquidity from LP and `reinvestL` is the liquidity from the fee. The liquidity L is the sum of these 2 variables. After each swap, the fee will be added into `reinvestL`.

### Approximation condition[​](https://docs.kyberswap.com/overview/elastic-walkthrough#approximation-condition) <a href="#approximation-condition" id="approximation-condition"></a>

Assume that fee = 1% and the swap results in less than a 5% change in price, we have:&#x20;

$${\Large \frac{\Delta x * fee}{x} } <  0.0005$$&#x20;

Alternatively, it is also possible to approximate based on tick calculation for swaps that have less than 5% price impact whereby a 5% change in price is equivalent to **487** ticks.

For swaps which result in price changes greater than 5%, we can dived it into multiple steps whereby each step is limited to a 5% price change.

### Reinvestment token[​](https://docs.kyberswap.com/overview/elastic-walkthrough#reinvestment-token) <a href="#reinvestment-token" id="reinvestment-token"></a>

* The **reinvestment token** represents the proportional share of the fee liquidity, `reinvestL`, that each user is entitled to.
* Reinvestment tokens are minted each time a user adds/removes liquidity or if a user's position crosses a tick. The amount of reinvestment tokens minted is equivalent to the additional fee liquidity, `reinvestL`, brought about by the changes in LP liquidity, `baseL`.
* Following the London Hardfork, warming up another contract became increasingly [costly](https://hackmd.io/@fvictorio/gas-costs-after-berlin). In order to reduce gas overheads, we have merged the reinvestment token and pool contract. Consequently, the pool contract inherits the ERC20 contract.
