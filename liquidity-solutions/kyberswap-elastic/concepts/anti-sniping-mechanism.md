---
description: Protecting Against Front-Runners
---

# Anti-Sniping Mechanism

## Introduction

As more value started to accrue towards DeFi, a new opportunity for value extraction arose based on how orders were prioritized on a public blockchain. As it takes time for a transaction to be finalized (i.e. added to a block), front runners could capitalize on the pending transaction whose information was publicly available. This practice came to be known as Maximal Extractable Value (MEV) and more details can be found [here](../../../getting-started/foundational-topics/decentralized-finance/maximal-extractable-value-mev.md).

Specific to AMMs, sniping is a specific form of MEV whereby an attacker jumps in front of normal liquidity providers by adding and removing liquidity just before and right after a huge swap. To protect our LPs, KyberSwap Elastic comes with an anti-sniping feature to natively protect them from any potential front-runners.

## Motivation[​](https://docs.kyberswap.com/overview/elastic-walkthrough#motivation) <a href="#motivation" id="motivation"></a>

New AMM, which compounds different positions such as Uniswap v3, provides tools for liquidity providers to add and remove liquidity easily in specific ranges. The feature leads to a novel attack, called sniping, where the attacker tries to jump in front of normal liquidity providers by adding and removing liquidity just before and right after a huge swap.

We have collected some [data](https://docs.google.com/document/d/1F50RWQRRyaNxnW5RvKgw09fN2FofIVLVccijgcOt-Iw/edit#heading=h.f4dlsc528bn4) to show the impact of the attack.

The sandwich attack can be effectively restrained on the taker's side thanks to parameters limiting how much slippage can be tolerated. However, there is no similar anti-sniping attack mechanism for liquidity providers. Hence, the protocol should introduce a feature that protects liquidity providers from this type of attack.

**KyberSwap Elastic's Anti-Sniping Feature** is introduced as a lock of reward, which is vested based on the duration of liquidity contribution. The principal difference between attacks and normal activities of liquidity providers is their contribution duration. When liquidity providers supply their funds to the protocol, they take the risk of impermanent loss. However, in the case of an attacker who withdraws their fund immediately, the impermanent loss can be pre-calculated so that their profit is guaranteed.

## Mechanism[​](https://docs.kyberswap.com/overview/elastic-walkthrough#mechanism) <a href="#mechanism" id="mechanism"></a>

### **Struct: Data**[**​**](https://docs.kyberswap.com/overview/elastic-walkthrough#struct-data)

| Field            | Type     | Explanation                         |
| ---------------- | -------- | ----------------------------------- |
| `lastActionTime` | `uint32` | timestamp of last action performed  |
| `lockTime`       | `uint32` | average start time of lock schedule |
| `unlockTime`     | `uint32` | average unlock time of locked fees  |
| `feesLocked`     | `uint32` | locked rToken qty since last update |

### **Adding liquidity**[**​**](https://docs.kyberswap.com/overview/elastic-walkthrough#adding-liquidity)

When adding liquidity to a position, it updates [Data](anti-sniping-mechanism.md#struct-data) values for that position and calculates the amount of claimable reinvestment tokens to be sent to the user.

```
Claimable_fees = claimable_amount_of_collected_fees + claimable_amount_of_locked_fees
```

The values are calculates based on the **unlockTime**, **lockedTime**, **lastActionTime**, **currentTime**, **feesLocked** and **feeSinceLastAction**, the formula can be found [here](../contracts/elastic-peripheral-library-contracts.md#update).

### **Removing liquidity**[**​**](https://docs.kyberswap.com/overview/elastic-walkthrough#removing-liquidity)

When removing liquidity from a position, it updates [Data](anti-sniping-mechanism.md#struct-data) values for that position and calculates the amount of claimable reinvestment tokens, as well as the amount of reinvestment tokens to be burnt.

After calculating the claimable amount of fees, the burnt fees is calculated based on the amount of liquidity that user is withdrawing.

```
Burnt_fees = Claimable_fees * liquidity_delta / current_liquidity.
Claimable_fees = Claimable_fees - Burnt_fees
```

## Whitelisting PositionManager[​](https://docs.kyberswap.com/overview/elastic-walkthrough#whitelisting-positionmanager) <a href="#whitelisting-positionmanager" id="whitelisting-positionmanager"></a>

As we implement the Anti-Sniping Attack mechanism in the **PositionMananger** contract, we need to prevent users/contracts from interacting directly with **Pool** contracts. To do so, we allow only whitelisted **PositionManager** contracts to call the **mint** function.

We don't have the whitelisted check in the **burn** function because:

* Only the **PositionManager** holds positions in the **Pool** contracts, thus, users must interact with **PositionManager** to burn their positions.
* In case we upgrade to a new **PositionManager** contract, all previous **PositionManager** contracts should still be able to remove liquidity.

The **Factory** contract stores all whitelisted **PositionManager** contracts, and have a function called **isWhitelistedNFTManager(address)** for **Pool** contracts to check if an address is whitelisted. To make it flexible, the **Factory** can disable the whitelisting feature, i.e: the **isWhitelistedNFTManager** function will always return **true**.

## Example[​](https://docs.kyberswap.com/overview/anti-JIT-attack#example) <a href="#example" id="example"></a>

Let's take an example where we have a pool of Token0/Token1 with 3 positions and 5 ticks and the current price (Token0/Token1) is 1. The relationship between price and tick is:

$$
p(i)=1.0001^i
$$

### Swapping exact input of Token0 (amount NOT enough to cross tick)[​](https://docs.kyberswap.com/overview/anti-JIT-attack#swapping-exact-input-of-token0-amount-not-enough-to-cross-tick) <a href="#swapping-exact-input-of-token0-amount-not-enough-to-cross-tick" id="swapping-exact-input-of-token0-amount-not-enough-to-cross-tick"></a>

$$
\Delta_x=0.0001
$$

The next tick is 1 (t\_tmp(1)=-1). Calculate square root of price to cross the next tick. We will divide into two functions next if the price moves rightward else back if it moves leftward.

$$
\sqrt{p_{next\_step(1)}} = 1.0001^{-1/2}= 0.99995000375
$$

Calculate delta\_x\_tmp that we need to cross the next tick

$$
delta_{x_{tmp}} = \frac{2(l_p+l_f)(\sqrt{p}-\sqrt{p_{next\_step(1)}})}{2*\sqrt{p_{next\_step(1)}}-fee*\sqrt{p}}
\\=\frac{2*(16+3)(1-0.99995000375)}{1*(2* 0.99995000375-0.003*1)}
\\= 0.00095140342
$$

We see that delta\_x\_tmp > delta\_x so we do not cross any tick. Now we calculate the collected liquidity l\_c:

$$
L_c=fee*delta_x*\sqrt{p}/2
= 0.003*0.0001*1/2
= 1.5e-7
$$

And calculate the new sqrtPrice:

$$
\sqrt{p_{tmp}}=(l_p+l_f+l_c)/(\Delta_x+(l_p+l_f)/\sqrt{p})
\\=(16+3+1.5e-7)/(0.0001+(16+3)/1)
\\= 0.99999474476
$$

Then we calculate delta\_y which is the amount of output in token1.

$$
\Delta_y=(l_p+l_f+l_c)*\sqrt{p_{tmp}}-(l_p+l_f)*\sqrt{p}
\\=(16+3+1.5e-7)* 0.99999474476-(16+3)*1
\\=-0.00009969956
$$

The delta\_y is negative because this is the amount of token1 that taker will take out of the liquidity pool. Now we can update the current price of liquidity pool equal to the new sqrtPrice.

$$
\sqrt{p}=\sqrt{p_{tmp}}
$$

And the collected liquidity is added to the reinvestment liquidity:

$$
l_f=l_f+l_c=3+1.5e-7
$$

### Swap exact output of Token1 (amount enough to cross tick)[​](https://docs.kyberswap.com/overview/anti-JIT-attack#swap-exact-output-of-token1-amount-enough-to-cross-tick) <a href="#swap-exact-output-of-token1-amount-enough-to-cross-tick" id="swap-exact-output-of-token1-amount-enough-to-cross-tick"></a>

$$
\Delta_y=0.001
$$

The next tick is 1 (t\_tmp(1)=-1). Calculate square root of price to cross the next tick. We will divide into two functions next if the price moves rightward else back if it moves leftward.

$$
\sqrt{p_{next\_step(1)}} = 1.0001^{-1/2}= 0.99995000375
$$

Calculate delta\_y\_tmp that we need to cross the next tick

$$
\Delta_{y_{tmp}} = \frac{-(l_p+l_f)(\sqrt{p}-\sqrt{p_{next\_step}})(2\sqrt{p_{next\_step}}-fee(\sqrt{p}+\sqrt{p_{next\_step}}))}{2\sqrt{p_{next\_step}}-fee\sqrt{p}}
\\=-(16+3)*(1-0.99995000375)(2* 0.99995000375-0.003*(0.99995000375+1))/(2* 0.99995000375-0.003*1)
\\=-0.00094850171
$$

We see that -delta\_y\_tmp < delta\_y so we cross the next tick. Now we calculate the collected liquidity l\_c:

$$
L_c=\frac{(\Delta_{y_{tmp}}+\sqrt{p}(l_p+l_f))}{\sqrt{price_{next\_step}}}-(l_p+l_f)
\\=(-0.00094850171+1*(16+3))/(0.99995000375)-(16+3)
\\= 0.00000142711
$$

Then we can update the delta\_x:

$$
\Delta_x=(l_{p}+l_f+l_c)/\sqrt{p_{next\_step}}-(l_{p}+l_f)/\sqrt{p}
\\=(16+3+ 0.00000142711)/0.99995000375 - (16+3)/1
\\= 0.00095140342
$$

Now we calculate the rest amount of \Delta\_y need to be swapped:

$$
\Delta_{y_{r}}=\Delta_y+\Delta_{y_{tmp}}
\\=0.001-0.00094850171
\\= 0.00005149829
$$

Now we calculate the additional pool tokens will be minted:

$$
s_{mint}=l_p*l_c/(L_{f_{last}}(l_p+l_f))*s
=(16* 0.00000142711/(3*(16+ 3.00000142711)))*3
\\= 0.00000120177
$$

So we will update the total supply of the reinvestment tokens:

$$
s=s+s_{mint}=3+ 0.00000120177 = 3.00000120177
$$

Now we calculate the sqrt price of the next step:

$$
\sqrt{p_{next\_step(2)}} = 1.0001^{-2/2}= 0.99990000999
$$

When we cross to tick -2 we must also update liquidity of the pool - l\_p\_tmp. It will subtract the liquidity net of the tick. In this simple example, so l\_p\_tmp=l\_p=16, meanwhile the temporary liquidity of the reinvestment curve l\_f\_tmp=l\_f+l\_c=3.00000142711 Calculate delta\_y\_tmp that we need to cross the next tick

$$
\Delta_{y_{tmp}} = -\frac{(l_{p_{tmp}}+l_{f_{tmp}})(\sqrt{p_{next\_step(1)}}-\sqrt{p_{next\_step(2)}})(2\sqrt{p_{next\_step(2)}}-fee(\sqrt{p_{next\_step(1)}}+\sqrt{p_{next\_step(2)}}))}{2\sqrt{p_{next\_step(2)}}-fee\sqrt{p_{next\_step(1)}}}
\\=-(16+3.00000142711)(0.99995000375-0.99990000999)(2 0.99990000999-0.003*(0.99990000999 + 0.99995000375))/(2* 0.99990000999-0.003* 0.99995000375)
\\=-0.00094845454
$$

So -delta\_y\_tmp>delta\_y\_r, we do not cross one more tick. Then we move to next step to calculate the new amount of collected fee.

$$
L_c^2*\sqrt{p_{next\_step(1)}}*fee+ 2((l_{p_{tmp}}+l_{f_{tmp}})*fee *\sqrt{p_{next\_step(1)}} - (l_{p_{tmp}}+l_{f_{tmp}})*\sqrt{p_{next\_step(1)}} - \Delta_y)l_c+(l_{p_{tmp}}+l_{f_{tmp}})*fee*\Delta_y=0
\\
0.003* 0.99995000375*l_c^2+2*((16+ 3.00000142711)*0.003* 0.99995000375-(16+ 3.00000142711)* 0.99995000375-0.001)l_c+(16+ 3.00000142711)*0.003*0.001=0
\\ 0.00299985001*l_c^2 -37.8861086961*l_c+ 0.000057 =0
\\l_c=0.0000015045085390746784
$$

And calculate the new sqrtPrice:

$$
\sqrt{p_{tmp}}=(-\Delta_{y_{r}}+(l_{p_{tmp}}+l_{f_{tmp}})/\sqrt{p_{next\_step(1)}})/(l_{p_{tmp}}+l_{f_{tmp}}+l_c)
\\=(-0.00005149829 +(16+3.00000142711)* 0.99995000375)/(16+ 3.00000142711 + 0.0000015045085390746784)
\\=0.99994721413
$$

Then we calculate delta\_x which is the amount of input in token0.

$$
\Delta_x =\Delta_x + (l_{p_{tmp}}+l_{f_{tmp}}+l_c)/\sqrt{p_{tmp}}-(l_{p_{tmp}}+l_{f_{tmp}})/\sqrt{p_{next\_step(1)}}
\\= 0.00095140342+(16+ 3.00000142711 + 0.0000015045085390746784)/ 0.99994721413-(16+ 3.00000142711)/0.99995000375
\\=0.00100591624
$$

Now we calculate the additional pool tokens will be minted:

$$
s_{mint}=l_{p_{tmp}}*l_c/(L_{f_{tmp}}(l_p+l_{f_{tmp}}+l_c))*s
\\=(16* 0.0000015045085390746784/(3.00000142711*(16+ 3.00000142711+ 0.0000015045085390746784)))*3
\\= 0.00000126695
$$

So we will update the total supply of the reinvestment tokens:

$$
s=s+s_{mint}= 3.00000120177+ 0.00000126695=3.00000246872
$$

Now we can update the current price of the liquidity pool equal to the new sqrtPrice.

$$
\sqrt{p}=\sqrt{p_{tmp}}
$$

And the collected liquidity is added to the reinvestment liquidity:

$$
l_f=l_{f_{tmp}}+l_c= 3.00000142711 + 0.0000015045085390746784\\= 3.00000293162
$$

### Add liquidity[​](https://docs.kyberswap.com/overview/anti-JIT-attack#add-liquidity) <a href="#add-liquidity" id="add-liquidity"></a>

Liquidity provider add liquidity to the pool to price range from **0.99995000375 to 1.00004999875 (tick -1 to tick 1),** which means the current price is in the price range of the the position, the amount of liquidity to be added:

$$
\Delta_L=1
$$

Now we need to calculate delta\_x, delta\_y taken from user:

$$
\Delta_x=\frac{\Delta_l}{\sqrt{p}}-\frac{\Delta_l}{\sqrt{p_{tick_{upper}}}}=1/1-1/1.00004999875= 0.00004999625
\\\Delta_y=\Delta_l(\sqrt{p}-\sqrt{p_{tick_{lower}}})=1-0.99995000375= 0.00004999625
$$

When adding liquidity to a position, it updates data values for that position and calculates the amount of claimable reinvestment tokens to be sent to the user. In this case, we consider that there is a different between the last time balances of reinvestment curve has been updated. The new reinvestment liquidity l\_f 3.1 meanwhile the last time we updated the balances, the reinvestment liquidity l\_f\_last is 3. Now we calculate the additional pool tokens will be minted:

$$
s_{mint}=l_p(l_{f}-l_{f_{last}})/(L_{f_{last}}(l_p+l_f))*s
=(16*(3.1-3)/(3*(16+3.1)))*3= 0.0837696335
$$

So we will update the total supply of the reinvestment tokens:

$$
s=s+s_{mint}=3+ 0.0837696335 = 3.0837696335
$$

We also need to update the balances of every liquidity providers and the "last" reinvestment liquidity (l\_f\_last). Then we transfer the collected pool tokens from addressPool to the user if the amount of reinvestment tokens collected of the user is greater than 0.

### Remove liquidity[​](https://docs.kyberswap.com/overview/anti-JIT-attack#remove-liquidity) <a href="#remove-liquidity" id="remove-liquidity"></a>

Similar to add liquidity when removing liquidity from a position, it updates data values for that position and calculates the amount of claimable reinvestment tokens, as well as the amount of reinvestment tokens to be burnt. After calculating the claimable amount of fees, the burnt fees is calculated based on the amount of liquidity that user is withdrawing.
