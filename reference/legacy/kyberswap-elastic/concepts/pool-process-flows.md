---
description: Automating Tried And Tested Procedures
---

# Pool Process Flows

## Pool unlocking/initialization[​](https://docs.kyberswap.com/overview/elastic-walkthrough#pool-unlocking--initialization) <a href="#pool-unlocking--initialization" id="pool-unlocking--initialization"></a>

### Overview[​](https://docs.kyberswap.com/overview/elastic-walkthrough#overview) <a href="#overview" id="overview"></a>

No action (minting / burning / swaps) can be performed prior to pool initialization.

In addition to setting the initial sqrt price, a small amount of token0 and token1 is required to be seeded for the initialization of `reinvestL` to the value of `MIN_LIQUIDITY`. This is required to prevent division by zero in the `calcRMintQty()` function when swaps are performed. `MIN_LIQUIDITY` was chosen to be reasonably small enough to avoid calculation inaccuracies for swaps, and from taking unreasonably large capital amounts from the caller.&#x20;

As part of this anti-spam feature, Elastic allocates $$10^5$$ token weis as liquidity for the reinvestment curve. While this amount has been carefully selected to suit the majority of tokens, there are rare exceptions where token teams decide to implement tokens with less decimals for reasons of their own. For reference, the majority of ERC20 tokens (LINK, MATIC, ANKR, SHIB, etc.) are created with $$10^{18}$$ decimals, WBTC has  $$10^8$$ decimals, major stablecoin tokens like USDC/USDT have $$10^6$$ decimals.&#x20;

In cases where the token has a low decimal value and the per unit value of the token high, the amount taken might be of significant value (i.e. a token is created with $$10^2$$ decimals and each unit has a 1USD value, which results in  $$10^5$$ tokens with a value of 100USD being taken as an anti-spam feature). As a permissionless platform, KyberSwap supports the listing of all tokens which meet the ERC20 standard and as such, users are responsible for checking if their token falls into the aforementioned category.

## Minting and burning (add/remove liquidity)[​](https://docs.kyberswap.com/overview/elastic-walkthrough#minting-adding-liquidity-and-burning-removing-liquidity-flow) <a href="#minting-adding-liquidity-and-burning-removing-liquidity-flow" id="minting-adding-liquidity-and-burning-removing-liquidity-flow"></a>

### Overview[​](https://docs.kyberswap.com/overview/elastic-walkthrough#overview-1) <a href="#minting-adding-liquidity-and-burning-removing-liquidity-flow" id="minting-adding-liquidity-and-burning-removing-liquidity-flow"></a>

Adding and removing liquidity have very similar flows. One of the main differences is that `mint()` is possibly a permissioned function, but `burn()` is not. More information relating to the requirement for this can be found in [this section](anti-sniping-mechanism.md#whitelisting-positionmanager) on whitelisting position managers.

#### Implementation details[​](https://docs.kyberswap.com/overview/elastic-walkthrough#implementation-details) <a href="#implementation-details" id="implementation-details"></a>

* A simple check is performed to ensure that the requested liquidity amount to mint / burn is non-zero
* `_tweakPosition()` is called, which does the following:
  * Load the pool state into memory `poolData` (current price, tick and liquidity values)
  * Call `_syncFeeGrowth()` to update fee growth data. Mints reinvestment tokens if necessary
  * Call `_syncSecondsPerLiquidity()` to update seconds per liquidity data
  * The updated global values and `poolData` is passed into `_updatePosition()`
    * Updates (initializes) the lower and upper position ticks. Will insert or remove the tick from the linked list whenever necessary
    * Calculates feeGrowthInside and returns the amount of reinvestment tokens claimable by the position
  * Transfers the claimable reinvestment tokens to the position owner, if any
  * Calculates the token0 and token1 quantity required to be collected from (add liquidity) or sent to (remove liquidity) `msg.sender`. Will apply liquidity changes to pool liquidity if the specified position is active
* In the case of adding liquidity, a callback is made to collect the tokens
* Emit event

## Swap <a href="#swap-flow" id="swap-flow"></a>

### Overview[​](https://docs.kyberswap.com/overview/elastic-walkthrough#overview-2) <a href="#overview-2" id="overview-2"></a>

Like `KyberSwap Classic`, there are 4 different types of swaps available that a user can specify.

1. Swap _from_ a specified amount of token 0 (exactInput0)
2. Swap _from_ a specified amount of token 1 (exactInput1)
3. Swap _to_ a specified amount of token 0 (exactOutput0)
4. Swap _to_ a specified amount of token 1 (exactOutput1)

Swapping token 0 for token 1 (cases 1 and 4) cause the pool price and tick to move downwards, while swapping token 1 for token 0 (cases 2 and 3) cause the pool price and tick to move upwards.

In addition, the user can specify a price limit that the swap can reach. The minimum and maximum price limits a user can specify is `MIN_SQRT_RATIO + 1` and `MAX_SQRT_RATIO - 1`.

The algorithm exits when either the specified amount has been fully used, or if the price limit has been reached.

#### Implementation details[​](https://docs.kyberswap.com/overview/elastic-walkthrough#implementation-details-1) <a href="#implementation-details-1" id="implementation-details-1"></a>

The swap amount is a `int256` to implicitly suggest whether it is exact input (> 0) or exact output (< 0).

1. Fetch the initial pool state
   * $$L_{base​}$$ := pool.baseL (liquidity provided by positions)
   * $$L_{reinvest​}$$ := pool.reinvestL (liquidity from fees collected)
   * $$\sqrt{P_{current}}$$ := pool.sqrtP (current sqrt price of token1/token0)
   * $$t_c$$ := pool.currentTick (tick associated with pool price)
   * $$t_n$$ := pool.nextTick (next initialized tick from current tick)
2. Verify specified price limit $$\sqrt{P_{lim}}$$
   * Cases 1 & 4: `MIN_SQRT_RATIO` < $$\sqrt{P_{lim}}$$ < $$\sqrt{P_{current}}$$
   * Cases 2 & 3: $$\sqrt{P_{current}}$$ < $$\sqrt{P_{lim}}$$ < `MAX_SQRT_RATIO`
3. While specified amount $$delta_{remaining}$$ not used up or price limit not reached,
   * Calculate temp next tick $$t_{tmp}$$ and next sqrt price $$\sqrt{P_{next}}$$. The temporary next tick is to ensure that the next tick does not exceed the MAX\_TICK\_DISTANCE cap from the current tick, so as not to violate the 5% price difference requirement.
     * $$\sqrt{P_{next}}$$ = TickMath.getSqrtRatioAtTick($$t_{tmp}$$)
   * Check if $$\sqrt{P_{next}}$$ exceeds $$\sqrt{P_{lim}}$$,
     * If true then $$\sqrt{P_{target}}$$ = $$\sqrt{P_{lim}}$$
     * If false then $$\sqrt{P_{target}}$$ = $$\sqrt{P_{next}}$$
   * Call `SwapMath.computeSwapStep()` to calculate the actual swap input and output amounts to be used, swap fee amount and next pool price
     * Subtract amount to be used (`usedAmount`) to `swapData.specifiedAmount`
     * Add amount to be sent to user (`returnedAmount`) to `swapData.returnedAmount`
     * Add collected swap fee $$\Delta{L}$$ to $$L_{reinvest}$$
   * Check if swap will reach next tick
     * If true, set `swapData.currentTick = willUpTick ? tempNextTick : tempNextTick - 1` and continue
     * If false, recalculate the current tick based on current price and break the loop
   * If $$t_{tmp}$$ == $$t_n$$, **we are crossing tick** $$t_n$$:
     * Load variables (if not loaded already) that are initialized when crossing ticks
     * Calculate amount of reinvestment tokens to be minted for fees to be sent to government and to for LP contributions, and update feeGrowthGlobal
     * Cross tick $$t_n$$: updates the tick outside values and apply tick.liquidityNet to pool liquidity whilst fetching the next tick $$t_n$$
4. Perform actual minting of reinvestment tokens if necessary
5. Update pool state (price, ticks, liquidity, feeGrowth, reinvestment variables)
6. Send token to caller, execute swap callback to collect token
   * Negative quantity = transfer to caller
   * Positive quantity = collect from caller

#### `computeSwapStep()` Flow[​](https://docs.kyberswap.com/overview/elastic-walkthrough#computeswapstep-flow) <a href="#computeswapstep-flow" id="computeswapstep-flow"></a>

**Inputs**[**​**](https://docs.kyberswap.com/overview/elastic-walkthrough#inputs)

| Field             | Type      | Explanation                                                                                          |
| ----------------- | --------- | ---------------------------------------------------------------------------------------------------- |
| `liquidity`       | `uint256` | active base liquidity + reinvestment liquidity                                                       |
| `currentSqrtP`    | `uint160` | current sqrt price                                                                                   |
| `targetSqrtP`     | `uint160` | sqrt price limit `nextSqrtP` can take                                                                |
| `feeInBps`        | `uint256` | swap fee in basis points                                                                             |
| `specifiedAmount` | `int256`  | amount remaining to be used for the swap                                                             |
| `isExactInput`    | `bool`    | true if `specifiedAmount` refers to input amount, false if `specifiedAmount` refers to output amount |
| `isToken0`        | `bool`    | true if `specifiedAmount` is in token0, false if `specifiedAmount` is in token1                      |

**Outputs**[**​**](https://docs.kyberswap.com/overview/elastic-walkthrough#outputs)

| Field            | Type      | Explanation                                                                                              |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| `usedAmount`     | `int256`  | actual amount to be used for the swap. >= 0 if `isExactInput` = true, <= 0 if `isExactInput` = false     |
| `returnedAmount` | `int256`  | output qty (<= 0) to be accumulated if `isExactInput` = true, input qty (>= 0) if `isExactInput` = false |
| `deltaL`         | `uint256` | collected swap fee, to be incremented to reinvest liquidity                                              |
| `nextSqrtP`      | `uint160` | new sqrt price after the computed swap step                                                              |

1. Calculate the amount required to reach `targetSqrtP` from `currentSqrtP` by calling `calcReachAmount()`.
2. If amount required exceeds `specifiedAmount`, then the targetPrice will not be reached, and we expect the resulting price `nextSqrtP` to not exceed `targetSqrtP`.
   * `usedAmount := specifiedAmount`
   * Estimate $$\Delta{L}$$, the swap fee to be collected by calling `estimateIncrementalLiquidity()`
   * Calculate the final price `nextSqrtP` by calling `calcFinalPrice()`
3. Otherwise, the temporary next tick will be crossed.
   * `usedAmount` will be the amount calculated in step 1
   * calculate $$\Delta{L}$$ by calling `calcIncrementalLiquidity()`
   * set the resulting price `nextSqrtP` = `targetSqrtP`
4. Finally, calculate `returnedAmount` by calling `calcReturnedAmount()`.

### Swapping formula[​](https://docs.kyberswap.com/explanation/appendix#appendix-d-swapping-formula) <a href="#appendix-d-swapping-formula" id="appendix-d-swapping-formula"></a>

Assume that:

* x1, x2: the amount of token0 before/after swap
* y1, y2: the amount of token1 before/after swap
* L1, L2: the liquidity before/after swap
* p1, p2: the price before/after swap

#### Swap exact input from token0 -> token1[​](https://docs.kyberswap.com/explanation/appendix#swap-exact-input-from-token0---token1) <a href="#swap-exact-input-from-token0---token1" id="swap-exact-input-from-token0---token1"></a>

* Given L1, p1, fee and $$\Delta y$$, calculate $$\Delta L$$ and p2

$$\Delta L = {L_1 * {\Large {\Delta y * fee \over 2 * y1}}}$$**(1)**

$$\Delta L = {\Large {\Delta y * fee  \over 2 * \sqrt p_1}}$$

Finally calculate new $$\sqrt{p_2}$$

&#x20;$$\sqrt{p_2} = \Large {y_1 + \Delta y \over L_2}$$ **(2)**

$$\sqrt{p_2} = \Large {L1 * \sqrt p1 + \Delta y \over L1 + \Delta L}$$

* Given L1, p1 and p2 calculate the $$\Delta L$$ and $$\Delta y$$

From (2) we have:$$\sqrt p_2 * (L1 + \Delta x * \sqrt p_1) = \sqrt p_1 * (L1 + \Delta L)$$ combine with (1)

$$2 * \sqrt p_2 * (L1 + \Delta x * \sqrt p_1) = \sqrt p_1 * ( 2 * L1 + \Delta x * fee * \sqrt p_1$$

\=> $$\Delta x * \sqrt p1 * (2 * \sqrt p_2 - fee * \sqrt p_1) = 2 * L1 * (\sqrt p_1 - \sqrt p_2)$$

\=> **(3)** $$\Delta x = \Large {\frac{2 * L1 * (\sqrt p_1 - \sqrt p_2)}{\sqrt p_1 * (2 * \sqrt p_2 - fee * \sqrt p_1)} }$$

#### Swap exact input from token1 -> token0[​](https://docs.kyberswap.com/explanation/appendix#swap-exact-input-from-token1---token0) <a href="#swap-exact-input-from-token1---token0" id="swap-exact-input-from-token1---token0"></a>

* Given L1, p1, fee and $$\Delta y$$, calculate $$\Delta L$$ and p2

$$\Delta L = {L_1 * {\Large {\Delta y * fee \over 2 * y1}}}$$**(1)**

$$\Delta L = {\Large {\Delta y * fee  \over 2 * \sqrt p_1}}$$

Finally calculate new $$\sqrt{p_2}$$&#x20;

$$\sqrt{p_2} = \Large {y_1 + \Delta y \over L_2}$$**(2)**

$$\sqrt{p_2} = \Large {L1 * \sqrt p1 + \Delta y \over L1 + \Delta L}$$

* Given L1, p1 and p2 calculate the $$\Delta L$$ and $$\Delta y$$

From (1) and (2) $$\sqrt p_2 * (L1 + {\Large {\Delta y * fee  \over 2 * \sqrt p_1}}) = L1 * \sqrt p1 + \Delta y$$

\=> $$\Delta y * (2 * \sqrt p_1 - fee * \sqrt p_2) = 2 * \sqrt p_1 * L1 * (\sqrt p_2 - \sqrt p_1)$$

\=> **(3)** $$\Delta y = \Large {2 * \sqrt p_1 * L1 * (\sqrt p_2 - \sqrt p_1) \over (2 * \sqrt p_1 - fee * \sqrt p_2)}$$

#### Swap exact output from token0 -> token1 (isExactInput = false, isToken0 = false)[​](https://docs.kyberswap.com/explanation/appendix#swap-exact-output-from-token0---token1-isexactinput--false-istoken0--false) <a href="#swap-exact-output-from-token0---token1-isexactinput--false-istoken0--false" id="swap-exact-output-from-token0---token1-isexactinput--false-istoken0--false"></a>

* Given L1, p1 and p2, calculate the $$\Delta y$$

$$y1 - \Delta y = L2 * \sqrt p_2$$

\=> $$\Delta y = \Delta L * \sqrt p_2 + L1 * (\sqrt p_2 - \sqrt p_1)$$

\=> $$\Delta y = {\Large \frac{\Delta x * fee * \sqrt p_1}{2}} * \sqrt p_2 + L1 * (\sqrt p_2 - \sqrt p_1)$$

\=> $$\Delta y = {\Large \frac{fee * \sqrt p_1 * L1 * (\sqrt p_1 - \sqrt p_2)}{\sqrt p_1 * (2 * \sqrt p_2 - fee * \sqrt p_1)}} * \sqrt p_2 + L1 * (\sqrt p_2 - \sqrt p_1)$$

\=> $$\Delta y = {\Large \frac{L1 (\sqrt p_1 - \sqrt p_2) (2 * \sqrt p_2 - fee * \sqrt p_1 - fee * \sqrt p_2)}{2 * \sqrt p_2 - fee * \sqrt p_1}}$$

* Given L1, p1 and $$\Delta y$$, calculate $$\Delta L$$

$$(L1 + \Delta L)^2 = (y1 - \Delta y) * (x1 + \Delta x)$$

\=> $$(L1 + \Delta L)^2 = (y1 - \Delta y) * (x1 + {\Large \frac{2 * \Delta L}{\sqrt p_1 * fee}})$$

\=> $$(L1 + \Delta L)^2 * fee = L1^2 * fee - fee * \Delta y * L1 / \sqrt p_1 + {\Large \frac{2 * \Delta L}{\sqrt p_1}} * (L1 / \sqrt p_1 - \Delta y)$$

\=> $$fee * \Delta L^2 - 2 * (L1 - fee * L1 - \Delta y  / \sqrt p_1) * \Delta L + L1 * fee * \Delta y / \sqrt p_1 = 0$$

This can be transformed into

&#x20;$$a * \Delta L ^2 - 2 * b * \Delta L + c = 0$$

&#x20;$$\Delta L$$ will be the smaller solution of this equation

#### Swap exact output token1 -> token0 (isExactInput = false, isToken0 = true)[​](https://docs.kyberswap.com/explanation/appendix#swap-exact-output-token1---token0-isexactinput--false-istoken0--true) <a href="#swap-exact-output-token1---token0-isexactinput--false-istoken0--true" id="swap-exact-output-token1---token0-isexactinput--false-istoken0--true"></a>

* Given L1, p1 and p2, calculate the $$\Delta x$$

$$x1 - \Delta x = L2 / \sqrt p_2$$

\=> $$\Delta x =  {\Large \frac{L1}{\sqrt p_1} -  \frac{\Delta L}{\sqrt p_2} - \frac{L1}{\sqrt p_2}}$$

\=> $$\Delta x = {\Large \frac{L1}{\sqrt p_1} - \frac{L1}{\sqrt p_2} -  \frac{\Delta y * fee}{ 2 * \sqrt p_1 * \sqrt p_2}}$$

\=> $$\Delta x = {\Large  \frac{L1}{\sqrt p_1} - \frac{L1}{\sqrt p_2} - {2 * \sqrt p_1 * L1 * (\sqrt p_2 - \sqrt p_1) \over (2 * \sqrt p_1 - fee * \sqrt p_2)} * \frac{fee}{2 * \sqrt p_1 * \sqrt p_2}}$$

\=> $$\Delta x = {\Large \frac{L1 * (\sqrt p_2 - \sqrt p_1)}{\sqrt p_2 * \sqrt p_1} * (1 - \frac{fee * \sqrt p_1}{2 * \sqrt p_1 - fee * \sqrt p_2})}$$

\=> $$\Delta x = {\Large \frac{L1 * (\sqrt p_2 - \sqrt p_1) * (2 * \sqrt p_1 - fee * \sqrt p_2 - fee * \sqrt p_1)}{\sqrt p_2 * \sqrt p_1 * (2 * \sqrt p_1 - fee * \sqrt p_2)}}$$

* Given L1, p1 and $$\Delta x$$, calculate $$\Delta L$$

$$(L1 + \Delta L)^2 = (x1 - \Delta x)(y1 + \Delta y)$$

\=> $$(L1 + \Delta L)^2 = L1 ^ 2 - \Delta x * L1 * \sqrt p_1 + \Delta y * (L1 / \sqrt p_1 - \Delta x)$$

\=> $$(L1 + \Delta L)^2 = L1 ^ 2 - \Delta x * L1 * \sqrt p_1 + \Delta L * 2 * \sqrt p_1 /fee * (L1 / \sqrt p_1 - \Delta x)$$

\=> $$fee * \Delta L^2 - 2 * (L1 * (1 - fee) - \Delta x * \sqrt p_1) * \Delta L + \Delta x * L1 * \sqrt p_1 * fee=0$$
