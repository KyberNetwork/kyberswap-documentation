---
description: Concentrated Liquidity Farms
---

# Tick-Based Farming

## Introduction

As a tick-based automated market maker (AMM), KyberSwap Elastic enables greater capital efficiency by allowing users to provide liquidity to a pool within a [custom price range](concentrated-liquidity.md). This also means that liquidity contributed by an LP is no longer equally distributed across the same range as other LPs.

{% hint style="success" %}
#### Liquidity: Measuring LP contributions

Please refer to [this section](concentrated-liquidity.md#liquidity-tracking-lp-contributions-at-a-specific-price) on the liquidity concept if you would like to understand how concentrated liquidity AMM protocols keep track of LP contributions and how trading fees are distributed.
{% endhint %}

Therefore, this customizability makes the traditional liquidity mining mechanism (i.e. distributing farming rewards to all staking users in a pro-rata way) no longer reasonable as different proportions of each LP's contributed liquidity will support the active price. The risks taken by each user also varies greatly.

To tackle these challenges, KyberSwap Elastic introduced innovative liquidity mining (aka farming) mechanisms that are able to distribute farming rewards to users according to multiple factors:

* Active time of liquidity (Dynamic Farms)
* Supported trade volume (Dynamic Farms)
* Liquidity contributed to operator-specified farm ranges (Static Farms)

{% hint style="info" %}
#### Static Farms: Capital efficient rewards distribution

While both Dynamic and Static Farms achieves practical distribution of farming rewards, the core distribution mechanism differs between the two. Dynamic Farms takes an active position approach while Static Farms takes a weighted distribution approach based on fixed farming ranges. Based on this difference, Static Farms introduces the following benefits:

* Operator (i.e. reward admin) configured farming ranges with weighted rewards distribution&#x20;
* Farming rewards for inactive ranges depending on operator defined farm ranges
* Simpler user farming journey

The introduction of farming ranges enables more fine-grained control of reward incentives. Instead of allocating a fixed amount of rewards to a token pair and relying completely on market forces to determine the distribution, Static Farms allow reward operators to influence distribution of rewards between various price ranges. In effect, rewards can be utilized more effectively to incentivize liquidity provision to specific price ranges instead of just the current active price.
{% endhint %}

## Dynamic Farms

In the first version of Elastic Farming, all farms were setup based on 2 types of farming mechanisms.

### **Dynamic Farms Type 1 - Active time** **of your liquidity**

This type of Farm relies on a single factor:

* Total time your liquidity position has been active (aka in range) in the pool and supporting the current price of the pool

Once you stake your liquidity position(s) into a Dynamic Farm, we will start calculating your farming rewards based on whether your liquidity position(s) is currently active (i.e. supporting the current price of the pool). You will continue to accumulate farming rewards as long as your position is active. You will of course accumulate rewards in proportion to the dollar value of your liquidity position relative to other farmers.

If your liquidity position goes out of range (aka becomes inactive), you will stop accumulating farming rewards. This can happen if the current price of the pool moves significantly due to market changes. You will have to adjust the price range of your liquidity position so that it is again in range (aka active) and is supporting the current price of the pool.

<details>

<summary>Type 1 example</summary>

* _There is a KNC-USDT (Fee = 0.04%) liquidity pool. The current price of the pool is $5.0 (i.e. 1 KNC = 5 USDT)_
* _You provide $1000 liquidity to KNC-USDT (Fee = 0.04%) Elastic pool where you add liquidity in a range from $4.0 to $6.0. This means that as long as the current price of KNC-USDT remains within this range your liquidity position will remain active (aka in range)_
* _KNC-USDT (Fee = 0.04%) pool has a Farm where you can earn farming rewards. There is already a total of $50,000 staked into this farm_
* _You deposit and thereafter stake your NFT position (that represents your $1000 liquidity position) into the KNC-USDT (Fee = 0.04%) farm_
* _After staking, you will start accumulating farming rewards since your liquidity position is active in proportion to your liquidity position. In this case you will earn rewards based on your $1000 of the total $50,000 that is staked_
* _Now lets say the current price of KNC-USDT goes to $6.5. Your liquidity position is now inactive (aka out of range) as you only provided liquidity in the $4.0 - $6.0 price range. You will now stop accumulating farming rewards_
* _In order to start earning farming rewards again, you will have to unstake your liquidity position from the farm, withdraw it, remove the liquidity from the KNC-USDT pool and provide liquidity in the correct price range again (e.g. $4.0 to $7.0) so it supports the current price of the pool. Alternatively, you can wait for the current price of the KNC-USDT pool to go back within your price range of $4.0 to $6.0, so that your liquidity positions becomes active again._

</details>

### **Dynamic Farms Type 2 - Active time** **of your liquidity & target volume**

This type of Farm relies on an additional factor as compared to Type 1:

* Total time your liquidity position has been active (aka in range) in the pool and supporting the current price of the pool
* Trade volume supported by your liquidity position (indicated by the target Fee earned from the pool). The objective of Target Trade Volume is for the project that is giving out farming incentives to indicate the trading volume they would like each liquidity position to support before they receive farming rewards.

Once you stake your liquidity position(s) into a farm, we will start calculating your farming rewards based on:

1. Whether your liquidity position(s) is currently active and supporting the current price of the pool
2. Whether your liquidity position(s) has supported the required target volume by supporting the trading volume in the pool.

You will accumulate farming rewards at a reduced rate even if your liquidity position does not hit the full Target Volume. As soon as your position hits the full Target Volume, from thereafter, you will continue receiving 100% of the rewards for that liquidity position. You will of course accumulate rewards in proportion to the dollar value of your liquidity position relative to other farmers

If your liquidity position goes out of range (aka becomes inactive), you will stop accumulating farming rewards. This can happen if the current price of the pool moves significantly due to market changes. You will have to adjust the price range of your liquidity position so that it is again in range (aka active) and is supporting the current price of the pool.

In order to hit your full Target Volume faster, you may also have to adjust the price range of your liquidity position so that it is concentrated enough and consequently more trading volume of the pool is supported by your liquidity position.

<details>

<summary>Type 2 example</summary>

* _There is a KNC-USDT (Fee = 0.04%) liquidity pool. The current price of the pool is $5.0 (i.e. 1 KNC = 5 USDT)_
* _You provide $1000 liquidity to KNC-USDT (Fee = 0.04%) Elastic pool where you add liquidity in a range from $4.0 to $6.0. This means that as long as the current price of KNC-USDT remains within this range your liquidity position will remain active (aka in range)_
* _KNC-USDT (Fee = 0.04%) pool has a Farm where you can earn farming rewards. There is already a total of $50,000 staked into this farm_
* _You deposit and thereafter stake your NFT position (that represents your $1000 liquidity position) into the KNC-USDT (Fee = 0.04%) farm_
* _Even though your liquidity position is currently active and supporting the current price of the KNC-USDT pool, you may not be accumulating any farming rewards yet, because there is no trading volume going through your liquidity position. As traders start trading using your liquidity position in the KNC-USDT pool, you will start accumulating farming rewards since your liquidity position is both active and is supporting the trading volume of the pool. The more trades that use your liquidity in the pool, the faster you reach your full Target Volume. Once you unlock your full Target Volume (decided by the project giving out farming incentives), you will start accumulating maximum farming rewards based on your $1000 liquidity of the total $50,000 that is staked._
* _If the current price of the KNC-USDT (Fee = 0.04%) pool is $5.0, it might be better in this instance to make your price range $4.5 to $5.5 so that your liquidity is more concentrated and therefore more trades will use your liquidity position. This way you can hit the full Target Volume faster and start earning maximum farming rewards. Of course, there is a chance that your liquidity position may become inactive if current price of KNC-USDT moves outside of your price range._
* _Now lets say the current price of KNC-USDT goes to $6.5. Your liquidity position is now inactive (aka out of range) as you only provided liquidity in the $4.0 - $6.0 price range. You will now stop accumulating farming rewards_
* _In order to start earning farming rewards again, you will have to unstake your liquidity position from the farm, withdraw it, remove the liquidity from the KNC-USDT pool and provide liquidity in the correct price range again (e.g. $4.0 to $7.0) so it supports the current price of the pool. Alternatively, you can wait for the current price of the KNC-USDT pool to go back within your price range of $4.0 to $6.0, so that your liquidity positions becomes active again._

</details>

## Static Farms

In the earlier Dynamic Farms, one of the main tradeoffs of the design was that rewards were only distributed to liquidity positions supporting the active price of the pool. While this distribution is seemingly fair, it results in the following:

* Reward distribution is entirely dictated by market prices. This meant reward operators were unable to utilize their capital efficiently to incentivize liquidity provision at specific price ranges.
* LPs stopped earning any rewards on inactive positions. To continue earning rewards, LPs had to unstake and repeat the whole staking process again from scratch. This increases gas costs as well as the manual management overhead required.

To address the aforementioned pain points, Static Farms introduced a weighted farm range reward system which can be easily configured by the operator.

### Farming range: Configurable range rewards

Static Farms enables operators to define specific price ranges (i.e. farming range) within which LPs will earn weighted shares of the reward pool. In other words, rewards only accrue to LPs who are supporting the operator specified farming range regardless of whether the price range is active. By allowing reward ranges to be customizable, operators have more fine-grained control over how their rewards are being utilized as incentives.

Given this customizability, operators are also provided the option to create multiple farming ranges, each with a separate weight. Instead of having to commit all the rewards to a single price range, the total rewards can be split across multiple price ranges. Operators now have the power to proportionally distribute rewards within the same pool. This means that both operators and liquidity providers no longer have to split their liquidity across different pools due to varying farming structures.

It is crucial to note that this weighted distribution of farming rewards is independent of the active range (i.e. the active time of liquidity and target volume concepts covered in Dynamic Farms no longer applies in Static Farms). Rewards will be distributed solely based on having a liquidity position (either active/inactive) that encompasses the farming range specified by the operator. Rewards distribution within a farming range will be based on the proportion of liquidity which an LP contributes towards the farm. LPs continue to earn trading fees for their underlying position but earn farming rewards based on the proportion of liquidity contributed to a farming range.

### Static Farms concept in practice

Without diving too deep into the technicals, we can gain an appreciation of Static Farm concepts by walking through the farming process sequentially:

* Farm operator configures a farm with multiple reward ranges, each with an assigned weight. Farming ranges can overlap based on the operator's discretion.
* Liquidity providers are able to participate in farming rewards by staking their liquidity position to a specified farm range. The LPs underlying liquidity price range must cover the whole farm range in order to be eligible for rewards from that farm range. Each position can only be staked into a single farm range.
* For each position that is staked in the farm, the farm assigns a proportional share of the rewards based on the [liquidity](concentrated-liquidity.md#liquidity-tracking-lp-contributions-at-a-specific-price) contributed to the specific farm range as well as the total amount of time the position is staked in the farm. This calculation also takes into account the weight assigned for the selected farm range.
* The rewards accrued to a LP are calculated at the point of withdrawal. To find the reward for each staked position, the total farming rewards is then multiplied by the shares that have accumulated to that position. (i.e. if a staked position has 10 shares and the total shares issued across all farm ranges in a farm is 100, the position gets 10% of total pool rewards).

Effectively, rewards calculation can be simplified via viewing farming rewards in terms of shares whereby each staked position accumulates a share of the total rewards pool based on:

* Liquidity contributed to the farm range
* Staking duration in farm range
* Weight of selected farm range relative to other farm ranges in the farm

## Static Farms example

The example below walks you through how farming rewards are calculated in the case whereby there is a single staker vs multiple stakers. Through this example, you will be able to understand how farming rewards are proportioned between various positions.

#### Static Farm setup

A farm operator setups a `KNC-USDT` farm which runs for 2 weeks (1,209,600 seconds) with total rewards of 100,000`KNC`. The rewards are spread across the following 2 ranges, each with a weight configured by the farm operator.&#x20;

<table><thead><tr><th width="223">Farm range ID</th><th width="276">Farm range</th><th width="250">Weight</th></tr></thead><tbody><tr><td>A</td><td>0.75-0.80</td><td>2</td></tr><tr><td>B</td><td>0.80-0.85</td><td>5</td></tr></tbody></table>

Based on the weights specified, the farm operator intends to incentivize more liquidity to be added to the higher price ranges (assuming current `KNC` price of 0.76). LPs providing liquidity to the higher price ranges can expect to get a larger share of the total rewards based on the operator assigned weight.

### Single staker

#### Liquidity provision and staking in a farm range

Upon the farm becoming active, Alice decides to participate in the 0.75-0.80 farm range. Alice has an existing [concentrated liquidity](concentrated-liquidity.md) position worth USD1,000 in the `KNC-USDT` pool with a price range of 0.75-0.80 (assume tick-spacing of 0.01 for simplicity). Alice expects that `KNC` price will continue to trade within this range and hence does not change her position to continue earning trading fees.

{% hint style="info" %}
#### Farm range rewards eligibility

Do note that only liquidity positions whose price range covers the full range of the farm are eligible for farming rewards. For example, if Alice creates a position with a range of 0.75-.079, she would not be eligible for the the Farm A rewards.
{% endhint %}

#### Claiming rewards

For simplicity, we will assume that no other LPs entered the farm and hence Alice currently owns 100% of the farming reward share and is therefore eligible to all the farming rewards in proportion to the total time of her stake. If Alice stakes for the full period of the farm, she will get the full 100,000`KNC` farming rewards. Due to the time element of the farm, the rewards will also be proportioned based on the total amount of time that a position supports the farm range (i.e. if Alice enters the farm halfway through, she will only get half the rewards).

### Multiple stakers

#### Liquidity provision and staking in a farm range

Halfway through the farming period, Bob decides to also participate in the `KNC-USDT` farm and sees that Farm Range B has a higher weight. Bob decides to create a new [concentrated liquidity](concentrated-liquidity.md) position worth USD1,000 with a range of 0.75-0.85. Based on his liquidity position, Bob is eligible to stake in both farm ranges but decides to go with Farm Range B as it has a comparatively higher weight.

#### Calculating shares

With multiple stakers in the farm, the farm now needs to track the proportion of rewards going to each of the position staked by Alice and Bob. Currently, we have the following staked positions.

<table><thead><tr><th width="103.33333333333331">LP</th><th width="169">Position Range</th><th width="136">Position TVL</th><th>Farm Range staked</th></tr></thead><tbody><tr><td>Alice</td><td>0.75-0.80</td><td>USD1,000</td><td>A (Range: 0.75-0.80, Weight: 2)</td></tr><tr><td>Bob</td><td>0.75-0.85</td><td>USD1,000</td><td>B (Range: 0.75-0.85, Weight: 5)</td></tr></tbody></table>

To get the reward shares for each position, the protocol calculates the proportion of [liquidity](concentrated-liquidity.md#liquidity-tracking-lp-contributions-at-a-specific-price) that the position has contributed to the farm.&#x20;

This example glances over the exact calculation but the formula for the liquidity contributed, $$L$$, can be found in the [section](concentrated-liquidity.md#calculating-liquidity) or in the [Elastic Whitepaper](../../../getting-started/whitepapers.md#kyberswap-elastic). For every concentrated liquidity position, the TVL is distributed across the selected price range in accordance to the pool's price curve. Consequently, what is important to note is that $$L$$ indicates the proportion of liquidity that a position has contributed within the specified price range.

To get the liquidity value, we have the following parameters:

* $$Token0 =$$`KNC`
* $$Token0_{price}= 0.76$$
* $$Token1 =$$`USDT`
* $$Token1_{price} = 1.00$$
* $$currentPrice = 0.76$$ (current pool price)
* $$minPrice_{Alice} = 0.75$$, $$minPrice_{Bob} = 0.75$$ (position's lower range)
* $$maxPrice_{Alice} = 0.80$$, $$maxPrice_{Bob} = 0.85$$ (position's higher range)
* $$TVL_{Alice}=1,000$$, $$TVL_{Bob}=1,000$$

Using the [liquidity formula](tick-based-farming.md#calculating-liquidity), we get the following liquidity values assuming the current market price remains within the position's range:

$$
L_{Alice}=26,166.75
$$

$$
L_{Bob}=12,174.35
$$

Notice that $$L_{Alice}$$ is higher than $$L_{Bob}$$ even though their positions are of similar dollar value. This is because the TVL of Bob's position is spread over a wider range when compared to Alice's position. In other words, for the price ranges where Alice's and Bob's position overlaps, Alice contributes significantly more liquidity to support trades within her selected price range.

To get the farming reward shares, we then need to factor in the weight assigned to each farming range whereby:&#x20;

$$
share_A=weight_{FarmRange}*L_A
$$

As such, we get the following:

$$
share_{Farm}=share_{Alice}+share_{Bob}
$$

$$
share_{Farm}=(weight_{FarmRangeA}*L_{Alice})+(weight_{FarmRangeB}*L_{Bob})
$$

$$
share_{Farm}=(2*26,166.75)+(5*12,174.35)
$$

$$
share_{Farm}=52,333.5+60,871.75=113,205.25
$$

Finally, to obtain the final reward payout at withdrawal, remember that Alice has staked for the whole 2 week duration of the farm (1,209,600 seconds) while Bob only entered halfway (604,800 seconds). For simplicity, we assume both Alice and Bob withdraws after the farm ends leading to the following parameters:

* $$duration_{Farm}=1,209,600$$
* $$duration_{Alice}=1,209,600$$
* $$duration_{Bob}=604,800$$
* $$rewards_{pool}=100,000$$`KNC`

Using the above, we are then able to calculate the final rewards allocated to Alice:

$$
rewards_{Alice}=\frac{duration_{Alice}}{duration_{Farm}}*\frac{share_{Alice}}{share_{Farm}}*\frac{}{}rewards_{pool}
$$

$$
rewards_{Alice}=\frac{1,209,600}{1,209,600}*\frac{52,333.5}{113,205.25}*100,000=46,228KNC
$$

Likewise for Bob:

$$
rewards_{Bob}=\frac{604,800}{1,209,600}*\frac{60,871.75}{113,205.25}*100,000=26,885.57KNC
$$

Note that not all the rewards in the farm were distributed as the rewards have to take into account the time element of farm deposits and withdrawals.
