---
description: Capital Efficiency Through Amplified Liquidity
---

# Programmable Pricing Curves

## Introduction

Programmable pricing curves enable more of a LP's position to be utilized in the market making process therefore increasing potential yields while simultaneously reducing slippage. To put it more formally, dynamic pricing curve setups improves upon the capital efficiency of earlier constant product AMMs through amplifying liquidity based on the price correlation between assets in the pool.

As these programmable pricing curves are tailored for each pair, it enables the amplification of liquidity for more stable pairs which results in higher capital efficiency and lower slippage. The higher the asset correlation, the more opportunities for capital efficiency as liquidity can be concentrated within a narrower price range with less risk of the price going out of range.

## Amplification Factor (AMP)

Each pool implements a constant product curve of [virtual balances](virtual-balances.md) which is modified by an amplification factor that is specified by the user on initial [pool setup](../user-guides/classic-pool-creation.md). This amplification factor enables more capital to be utilized within an increasingly narrow price range (as opposed to 0 and ∞ for classic AMMs). The higher the amplification factor, the higher the potential yields withthe accompanying out of range risks (i.e. liquidity position goes out of range and is not earning fees). Consequently, higher amplification factors are recommended for more stable pairs and vice versa.

An amplification factor of 100 means that a pool of 1M USDC and 1M USDT will be able to achieve a spread and slippage equal to a standard pool of 100M USDC and 100M USDT, assuming the pool was started at the mean. This is a capital efficiency gain of 100X but it of course comes with a narrower price range within which fees are captured.

For each token pair, there are possibly many multiple pools with different configurations for the pricing curve. Pools are ready to accept one token for the other as long as KyberSwap's formula is preserved. A good approach to arrive at a suitable AMP is to look at the historical price correlation between the token pairs. This can be approximately quantified via 3 factors:

* **Ratio:** The price of token X in terms of token Y at a given point in time
* **Amplitude:** The max ratio divided by the min ratio across a given time period
* **Standard Deviation from Mean (σ):** The standard deviation of the mean of the ratios

Applying the above framework to our market observations, KyberSwap Classic defines 4 price correlation categories:

| Asset Pairs Price Stability | Sample Pairs                                | Recommended Amplification Factor |
| --------------------------- | ------------------------------------------- | -------------------------------- |
| Similar                     | <p>USDT/USDC<br>DAI/USDC<br>WBTC/renBTC</p> | 20 < AMP                         |
| Strongly Correlated         | <p>EURS/USDC<br>XSGD/USDC</p>               | 5 < AMP ≤ 20                     |
| Correlated                  | <p>WBTC/ETH<br>LINK/ETH</p>                 | 2 < AMP ≤ 5                      |
| Weakly Correlated           | <p>ZRX/ETH<br>AMPL/ETH<br>CAP/ETH</p>       | 1 ≤ AMP ≤ 2                      |

For recently-launched tokens which are not stablecoins, we recommend starting with an AMP of 1.1-1.25 for the pool.
