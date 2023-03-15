---
description: Concentrated Liquidity Farms
---

# Tick-Based Farming

## Introduction

As a tick-based automated market maker (AMM), KyberSwap Elastic enables greater capital efficiency by allowing users to provide liquidity to a pool within a [custom price range](concentrated-liquidity.md). This also means that liquidity contributed by an LP is no longer equally distributed across the same range as other LPs.

Therefore, this customizability makes the traditional liquidity mining mechanism (i.e. distributing farming rewards to all staking users in a pro-rata way) no longer reasonable as different proportions of each LP's contributed liquidity will support the active price. The risk taken by each user also varies greatly.

To tackle these challenges, KyberSwap Elastic introduced an innovative liquidity mining (aka farming) system that is able to distribute farming rewards to users according to their contribution to the pool's active liquidity. We’ve implemented 2 farming mechanisms, and all farms will be setup based on either of these farming mechanisms.

## Farming mechanisms

Lets look into these 2 types of farming mechanisms, as it will be important for liquidity providers (and farmers) to monitor their liquidity positions and adjust when needed to maximize their earnings through farming:

## **Farming Type 1 - Active time** **of your liquidity**

This type of Farm relies on a single factor:

* Total time your liquidity position has been active (aka in range) in the pool and supporting the current price of the pool

Once you stake your liquidity position(s) into a farm, we will start calculating your farming rewards based on whether your liquidity position(s) is currently active (i.e. supporting the current price of the pool). You will continue to accumulate farming rewards as long as your position is active. You will of course accumulate rewards in proportion to the dollar value of your liquidity position relative to other farmers.

If your liquidity position goes out of range (aka becomes inactive), you will stop accumulating farming rewards. This can happen if the current price of the pool moves significantly due to market changes. You will have to adjust the price range of your liquidity position so that it is again in range (aka active) and is supporting the current price of the pool.

#### Example

* _There is a KNC-USDT (Fee = 0.04%) liquidity pool. The current price of the pool is $5.0 (i.e. 1 KNC = 5 USDT)_
* _You provide $1000 liquidity to KNC-USDT (Fee = 0.04%) Elastic pool where you add liquidity in a range from $4.0 to $6.0. This means that as long as the current price of KNC-USDT remains within this range your liquidity position will remain active (aka in range)_
* _KNC-USDT (Fee = 0.04%) pool has a Farm where you can earn farming rewards. There is already a total of $50,000 staked into this farm_
* _You deposit and thereafter stake your NFT position (that represents your $1000 liquidity position) into the KNC-USDT (Fee = 0.04%) farm_
* _After staking, you will start accumulating farming rewards since your liquidity position is active in proportion to your liquidity position. In this case you will earn rewards based on your $1000 of the total $50,000 that is staked_
* _Now lets say the current price of KNC-USDT goes to $6.5. Your liquidity position is now inactive (aka out of range) as you only provided liquidity in the $4.0 - $6.0 price range. You will now stop accumulating farming rewards_
* _In order to start earning farming rewards again, you will have to unstake your liquidity position from the farm, withdraw it, remove the liquidity from the KNC-USDT pool and provide liquidity in the correct price range again (e.g. $4.0 to $7.0) so it supports the current price of the pool. Alternatively, you can wait for the current price of the KNC-USDT pool to go back within your price range of $4.0 to $6.0, so that your liquidity positions becomes active again._

### **Farming Type 2 - Active time** **of your Liquidity & target volume**

This type of Farm relies on an additional factor as compared to Type 1:

* Total time your liquidity position has been active (aka in range) in the pool and supporting the current price of the pool
* Trade volume supported by your liquidity position (indicated by the target Fee earned from the pool). The objective of Target Trade Volume is for the project that is giving out farming incentives to indicate the trading volume they would like each liquidity position to support before they receive farming rewards.

Once you stake your liquidity position(s) into a farm, we will start calculating your farming rewards based on:

1. Whether your liquidity position(s) is currently active and supporting the current price of the pool
2. Whether your liquidity position(s) has supported the required target volume by supporting the trading volume in the pool.

You will accumulate farming rewards at a reduced rate even if your liquidity position does not hit the full Target Volume. As soon as your position hits the full Target Volume, from thereafter, you will continue receiving 100% of the rewards for that liquidity position. You will of course accumulate rewards in proportion to the dollar value of your liquidity position relative to other farmers

If your liquidity position goes out of range (aka becomes inactive), you will stop accumulating farming rewards. This can happen if the current price of the pool moves significantly due to market changes. You will have to adjust the price range of your liquidity position so that it is again in range (aka active) and is supporting the current price of the pool.

In order to hit your full Target Volume faster, you may also have to adjust the price range of your liquidity position so that it is concentrated enough and consequently more trading volume of the pool is supported by your liquidity position.

#### Example

* _There is a KNC-USDT (Fee = 0.04%) liquidity pool. The current price of the pool is $5.0 (i.e. 1 KNC = 5 USDT)_
* _You provide $1000 liquidity to KNC-USDT (Fee = 0.04%) Elastic pool where you add liquidity in a range from $4.0 to $6.0. This means that as long as the current price of KNC-USDT remains within this range your liquidity position will remain active (aka in range)_
* _KNC-USDT (Fee = 0.04%) pool has a Farm where you can earn farming rewards. There is already a total of $50,000 staked into this farm_
* _You deposit and thereafter stake your NFT position (that represents your $1000 liquidity position) into the KNC-USDT (Fee = 0.04%) farm_
* _Even though your liquidity position is currently active and supporting the current price of the KNC-USDT pool, you may not be accumulating any farming rewards yet, because there is no trading volume going through your liquidity position. As traders start trading using your liquidity position in the KNC-USDT pool, you will start accumulating farming rewards since your liquidity position is both active and is supporting the trading volume of the pool. The more trades that use your liquidity in the pool, the faster you reach your full Target Volume. Once you unlock your full Target Volume (decided by the project giving out farming incentives), you will start accumulating maximum farming rewards based on your $1000 liquidity of the total $50,000 that is staked._
* _If the current price of the KNC-USDT (Fee = 0.04%) pool is $5.0, it might be better in this instance to make your price range $4.5 to $5.5 so that your liquidity is more concentrated and therefore more trades will use your liquidity position. This way you can hit the full Target Volume faster and start earning maximum farming rewards. Of course, there is a chance that your liquidity position may become inactive if current price of KNC-USDT moves outside of your price range._
* _Now lets say the current price of KNC-USDT goes to $6.5. Your liquidity position is now inactive (aka out of range) as you only provided liquidity in the $4.0 - $6.0 price range. You will now stop accumulating farming rewards_
* _In order to start earning farming rewards again, you will have to unstake your liquidity position from the farm, withdraw it, remove the liquidity from the KNC-USDT pool and provide liquidity in the correct price range again (e.g. $4.0 to $7.0) so it supports the current price of the pool. Alternatively, you can wait for the current price of the KNC-USDT pool to go back within your price range of $4.0 to $6.0, so that your liquidity positions becomes active again._
