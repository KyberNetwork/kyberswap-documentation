# Elastic Core Libraries

## BaseSplitCodeFactory[​](https://docs.kyberswap.com/explanation/core-libraries#basesplitcodefactory) <a href="#basesplitcodefactory" id="basesplitcodefactory"></a>

Inherited by the Factory contract. Main purpose is to hold the Kyberswap Elastic Pool creation code in a separate address, since its creation code is close to the bytecode size limit of 24kB.

Taken from [Balancer Labs's solidity utils repo](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/solidity-utils/contracts/helpers/BaseSplitCodeFactory.sol). The only modification made is the unchecked keyword for sol 0.8 compatibility.

### `getCreationCodeContracts()`[​](https://docs.kyberswap.com/explanation/core-libraries#getcreationcodecontracts) <a href="#getcreationcodecontracts" id="getcreationcodecontracts"></a>

Returns the 2 addresses where the creation code of the contract created by this factory is stored.

### `getCreationCode()`[​](https://docs.kyberswap.com/explanation/core-libraries#getcreationcode) <a href="#getcreationcode" id="getcreationcode"></a>

Returns the creation code of the contract this factory creates.

## CodeDeployer[​](https://docs.kyberswap.com/explanation/core-libraries#codedeployer) <a href="#codedeployer" id="codedeployer"></a>

Taken from [Balancer Labs's solidity utils repo](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/solidity-utils/contracts/helpers/CodeDeployer.sol). Imported and used by the [`BaseSplitCodeFactory`](elastic-core-libraries.md#basesplitcodefactory) contract to handle deployment.

## FullMath[​](https://docs.kyberswap.com/explanation/core-libraries#fullmath) <a href="#fullmath" id="fullmath"></a>

Taken from [Mathemagic finale: muldiv](https://xn--2-umb.com/21/muldiv) - _Remco Bloeman_. Facilitates multiplication and division that can have overflow of an intermediate value without any loss of precision. Handles "phantom overflow" i.e., allows multiplication and division where an intermediate value overflows 256 bits.

### `mulDivFloor()`[​](https://docs.kyberswap.com/explanation/core-libraries#muldivfloor) <a href="#muldivfloor" id="muldivfloor"></a>

Returns `(a * b / denominator)` rounded down.&#x20;

| Input         | Type      | Explanation  |
| ------------- | --------- | ------------ |
| `a`           | `uint256` | multiplicand |
| `b`           | `uint256` | multiplier   |
| `denominator` | `uint256` | divisor      |

### `mulDivCeiling()`[​](https://docs.kyberswap.com/explanation/core-libraries#muldivceiling) <a href="#muldivceiling" id="muldivceiling"></a>

Similar to [`mulDivFloor`](elastic-core-libraries.md#muldivfloor), but rounded up.

## LinkedList[​](https://docs.kyberswap.com/explanation/core-libraries#linkedlist) <a href="#linkedlist" id="linkedlist"></a>

A doubly linked list to be used for tick management.

### Struct: Data[​](https://docs.kyberswap.com/explanation/core-libraries#struct-data) <a href="#struct-data" id="struct-data"></a>

| Field      | Type    | Explanation   |
| ---------- | ------- | ------------- |
| `previous` | `int24` | previous tick |
| `next`     | `int24` | next tick     |

### `init()`[​](https://docs.kyberswap.com/explanation/core-libraries#init) <a href="#init" id="init"></a>

Initializes the LinkedList with the lowestValue and highestValue, where

* `lowestValue.previous = lowestValue`
* `lowestValue.next` = `highestValue`
* `highestValue.previous = lowestValue`
* `highestValue.next = highestValue`

| Field          | Type                     | Explanation                                      |
| -------------- | ------------------------ | ------------------------------------------------ |
| `self`         | `mapping(int24 => Data)` | A mapping of `int24` values to the `Data` struct |
| `lowestValue`  | `int24`                  | lowest value                                     |
| `highestValue` | `int24`                  | highest value                                    |

### `insert()`[​](https://docs.kyberswap.com/explanation/core-libraries#insert) <a href="#insert" id="insert"></a>

Inserts a new value into the LinkedList, given an existing lower value. The new value to be inserted should not be an existing value. Also, the condition `lowerValue < newValue < lowerValue.next` should be satisfied.

| Field        | Type                     | Explanation                                                    |
| ------------ | ------------------------ | -------------------------------------------------------------- |
| `self`       | `mapping(int24 => Data)` | A mapping of `int24` values to the `Data` struct               |
| `newValue`   | `int24`                  | value to be inserted                                           |
| `lowerValue` | `int24`                  | highest existing value in the linked list that is `< newValue` |

### `remove()`[​](https://docs.kyberswap.com/explanation/core-libraries#remove) <a href="#remove" id="remove"></a>

Removes an existing value from the LinkedList. Returns the next lowest value (`existingValue.previous`).

Note that no removal is performed if `removedValue` happens to be the `lowestValue` or `highestValue` passed in [`init()`](elastic-core-libraries.md#init).

| Field          | Type                     | Explanation                                      |
| -------------- | ------------------------ | ------------------------------------------------ |
| `self`         | `mapping(int24 => Data)` | A mapping of `int24` values to the `Data` struct |
| `removedValue` | `int24`                  | value to be removed                              |

## LiqDeltaMath[​](https://docs.kyberswap.com/explanation/core-libraries#liqdeltamath) <a href="#liqdeltamath" id="liqdeltamath"></a>

Contains a function to assist with the addition of signed liquidityDelta to unsigned liquidity.

### `applyLiquidityDelta()`[​](https://docs.kyberswap.com/explanation/core-libraries#applyliquiditydelta) <a href="#applyliquiditydelta" id="applyliquiditydelta"></a>

Adds or remove `uint128` liquidityDelta to `uint128` liquidity&#x20;

| Field            | Type      | Explanation                                    |
| ---------------- | --------- | ---------------------------------------------- |
| `liquidity`      | `uint128` | Liquidity to be adjusted                       |
| `liquidityDelta` | `int128`  | quantity change to be applied                  |
| `isAddLiquidity` | `bool`    | true = add liquidity, false = remove liquidity |

## MathConstants[​](https://docs.kyberswap.com/explanation/core-libraries#mathconstants) <a href="#mathconstants" id="mathconstants"></a>

Contains constants commonly used by multiple files.

## QtyDeltaMath[​](https://docs.kyberswap.com/explanation/core-libraries#qtydeltamath) <a href="#qtydeltamath" id="qtydeltamath"></a>

Contains functions for calculating token0 and token1 quantites from differences in prices or from burning reinvestment tokens

### `getQtysForInitialLockup()`[​](https://docs.kyberswap.com/explanation/core-libraries#getqtysforinitiallockup) <a href="#getqtysforinitiallockup" id="getqtysforinitiallockup"></a>

Calculate the token0 and token1 quantities needed for unlocking the pool given an initial price and liquidity.&#x20;

**Input**

| Input Field    | Type      | Explanation                                           |
| -------------- | --------- | ----------------------------------------------------- |
| `initialSqrtP` | `uint160` | initial sqrt price raised by `2**96`                  |
| `liquidity`    | `uint128` | initial liquidity. should be `MIN_LIQUIDITY = 100000` |

**Output**

| Return Field | Type      | Explanation              |
| ------------ | --------- | ------------------------ |
| `qty0`       | `uint256` | token0 quantity required |
| `qty1`       | `uint256` | token1 quantity required |

### `calcRequiredQty0()`[​](https://docs.kyberswap.com/explanation/core-libraries#calcrequiredqty0) <a href="#calcrequiredqty0" id="calcrequiredqty0"></a>

Calculates the token0 quantity between 2 sqrt prices for a given liquidity quantity.

Note that the function assumes that `upperSqrtP > lowerSqrtP`.

**Input**[**​**](https://docs.kyberswap.com/explanation/core-libraries#input)

| Field            | Type      | Explanation                                    |
| ---------------- | --------- | ---------------------------------------------- |
| `lowerSqrtP`     | `uint160` | the lower sqrt price                           |
| `upperSqrtP`     | `uint128` | the upper sqrt price                           |
| `liquidity`      | `int128`  | liquidity quantity                             |
| `isAddLiquidity` | `bool`    | true = add liquidity, false = remove liquidity |

**Output**[**​**](https://docs.kyberswap.com/explanation/core-libraries#output)

| Type     | Explanation                                                               |
| -------- | ------------------------------------------------------------------------- |
| `int256` | token0 qty required for position with liquidity between the 2 sqrt prices |

Generally, if the return value > 0, it will be transferred into the pool. Conversely, if the return value < 0, it will be transferred out of the pool.

### `calcRequiredQty1()`[​](https://docs.kyberswap.com/explanation/core-libraries#calcrequiredqty1) <a href="#calcrequiredqty1" id="calcrequiredqty1"></a>

Calculates the token1 quantity between 2 sqrt prices for a given liquidity quantity.

Note that the function assumes that `upperSqrtP > lowerSqrtP`.

**Input**[**​**](https://docs.kyberswap.com/explanation/core-libraries#input-1)

| Field            | Type      | Explanation                                    |
| ---------------- | --------- | ---------------------------------------------- |
| `lowerSqrtP`     | `uint160` | the lower sqrt price                           |
| `upperSqrtP`     | `uint128` | the upper sqrt price                           |
| `liquidity`      | `int128`  | liquidity quantity                             |
| `isAddLiquidity` | `bool`    | true = add liquidity, false = remove liquidity |

**Output**[**​**](https://docs.kyberswap.com/explanation/core-libraries#output-1)

| Type     | Explanation                                                               |
| -------- | ------------------------------------------------------------------------- |
| `int256` | token0 qty required for position with liquidity between the 2 sqrt prices |

Generally, if the return value > 0, it will be transferred into the pool. Conversely, if the return value < 0, it will be transferred out of the pool.

### `getQty0FromBurnRTokens()`[​](https://docs.kyberswap.com/explanation/core-libraries#getqty0fromburnrtokens) <a href="#getqty0fromburnrtokens" id="getqty0fromburnrtokens"></a>

Calculates the token0 quantity to be sent to the user for a given amount of reinvestment tokens to be burnt.

| Input Field | Type      | Explanation                                                                         |
| ----------- | --------- | ----------------------------------------------------------------------------------- |
| `sqrtP`     | `uint160` | the current sqrt price                                                              |
| `liquidity` | `uint128` | expected change in reinvestment liquidity due to the burning of reinvestment tokens |

### `getQty1FromBurnRTokens()`[​](https://docs.kyberswap.com/explanation/core-libraries#getqty1fromburnrtokens) <a href="#getqty1fromburnrtokens" id="getqty1fromburnrtokens"></a>

Calculates the token1 quantity to be sent to the user for a given amount of reinvestment tokens to be burnt.

| Input Field | Type      | Explanation                                                                         |
| ----------- | --------- | ----------------------------------------------------------------------------------- |
| `sqrtP`     | `uint160` | the current sqrt price                                                              |
| `liquidity` | `uint128` | expected change in reinvestment liquidity due to the burning of reinvestment tokens |

### `divCeiling()`[​](https://docs.kyberswap.com/explanation/core-libraries#divceiling) <a href="#divceiling" id="divceiling"></a>

Returns `ceil(x / y)`. `y` should not be zero.

## QuadMath[​](https://docs.kyberswap.com/explanation/core-libraries#quadmath) <a href="#quadmath" id="quadmath"></a>

### `getSmallerRootOfQuadEqn()`[​](https://docs.kyberswap.com/explanation/core-libraries#getsmallerrootofquadeqn) <a href="#getsmallerrootofquadeqn" id="getsmallerrootofquadeqn"></a>

Given a variant of the quadratic equation $$ax^2 - 2bx + c - 0$$ where $$a$$, $$b$$ and $$c > 0$$, calculate the smaller root via the quadratic formula.

Returns $$\frac{b - \sqrt{b^2 - ac}}{a}$$&#x20;

| Input Field | Type      | Explanation |
| ----------- | --------- | ----------- |
| `a`         | `uint256` |             |
| `b`         | `uint256` |             |
| `c`         | `uint256` |             |

### `sqrt()`[​](https://docs.kyberswap.com/explanation/core-libraries#sqrt) <a href="#sqrt" id="sqrt"></a>

Unchanged from [DMMv1](https://github.com/dynamic-amm/smart-contracts/blob/master/contracts/libraries/MathExt.sol#L36-L48). Calculates the square root of a value using the Babylonian method.

## ReinvestmentMath[​](https://docs.kyberswap.com/explanation/core-libraries#reinvestmentmath) <a href="#reinvestmentmath" id="reinvestmentmath"></a>

Contains a helper function to calculate reinvestment tokens to be minted given an increase in reinvestment liquidity.

### `calcRMintQty()`[​](https://docs.kyberswap.com/explanation/core-libraries#calcrmintqty) <a href="#calcrmintqty" id="calcrmintqty"></a>

Given the difference between `reinvestL` and `reinvestLLast`, calculate how many reinvestment tokens are to be minted.&#x20;

$$rMintQty = rTotalSupply * \frac{reinvestL - reinvestL_{Last}}{reinvestL_{Last}} * \frac{baseL}{baseL + reinvestL}$$&#x20;

| Input Field     | Type      | Explanation                                                       |
| --------------- | --------- | ----------------------------------------------------------------- |
| `reinvestL`     | `uint256` | latest reinvestment liquidity value. Should be `>= reinvestLLast` |
| `reinvestLLast` | `uint256` | reinvestmentLiquidityLast value                                   |
| `baseL`         | `uint256` | active base liquidity                                             |
| `rTotalSupply`  | `uint256` | total supply of reinvestment token                                |

## SafeCast[​](https://docs.kyberswap.com/explanation/core-libraries#safecast) <a href="#safecast" id="safecast"></a>

Contains methods for safely casting between different types.

### `toUint32()`[​](https://docs.kyberswap.com/explanation/core-libraries#touint32) <a href="#touint32" id="touint32"></a>

Casts a `uint256` to a `uint32`. Reverts on overflow.

### `toInt128()`[​](https://docs.kyberswap.com/explanation/core-libraries#toint128) <a href="#toint128" id="toint128"></a>

Casts a `uint128` to a `int128`. Reverts on overflow.

### `toUint128()`[​](https://docs.kyberswap.com/explanation/core-libraries#touint128) <a href="#touint128" id="touint128"></a>

Casts a `uint256` to a `uint128`. Reverts on overflow.

### `revToUint128()`[​](https://docs.kyberswap.com/explanation/core-libraries#revtouint128) <a href="#revtouint128" id="revtouint128"></a>

Given `int128 y`, returns `uint128 z = -y`.

### `toUint160()`[​](https://docs.kyberswap.com/explanation/core-libraries#touint160) <a href="#touint160" id="touint160"></a>

Casts a `uint256` to a `uint160`. Reverts on overflow.

### `toInt256()`[​](https://docs.kyberswap.com/explanation/core-libraries#toint256) <a href="#toint256" id="toint256"></a>

Casts a `uint256` to a `int256`. Reverts on overflow.

### `revToInt256()`[​](https://docs.kyberswap.com/explanation/core-libraries#revtoint256) <a href="#revtoint256" id="revtoint256"></a>

Cast a `uint256` to a `int256` and reverses the sign. Reverts on overflow.

### `revToUint256()`[​](https://docs.kyberswap.com/explanation/core-libraries#revtouint256) <a href="#revtouint256" id="revtouint256"></a>

Given `int256 y`, returns `uint256 z = -y`.

## SwapMath[​](https://docs.kyberswap.com/explanation/core-libraries#swapmath) <a href="#swapmath" id="swapmath"></a>

Contains the logic needed for computing swap input / output amounts and fees. The primary function to look at is [`computeSwapStep`](elastic-core-libraries.md#computeswapstep), as it is where the bulk of the swap flow logic is in, and where calls to the other functions in the library are made.

### `computeSwapStep()`[​](https://docs.kyberswap.com/explanation/core-libraries#computeswapstep) <a href="#computeswapstep" id="computeswapstep"></a>

Computes the actual swap input / output amounts to be deducted or added, the swap fee to be collected and the resulting price.

**Inputs**[**​**](https://docs.kyberswap.com/explanation/core-libraries#inputs)

| Field             | Type      | Explanation                                                                                          |
| ----------------- | --------- | ---------------------------------------------------------------------------------------------------- |
| `liquidity`       | `uint256` | active base liquidity + reinvestment liquidity                                                       |
| `currentSqrtP`    | `uint160` | current sqrt price                                                                                   |
| `targetSqrtP`     | `uint160` | sqrt price limit `nextSqrtP` can take                                                                |
| `feeInBps`        | `uint256` | swap fee in basis points                                                                             |
| `specifiedAmount` | `int256`  | amount remaining to be used for the swap                                                             |
| `isExactInput`    | `bool`    | true if `specifiedAmount` refers to input amount, false if `specifiedAmount` refers to output amount |
| `isToken0`        | `bool`    | true if `specifiedAmount` is in token0, false if `specifiedAmount` is in token1                      |

**Outputs**[**​**](https://docs.kyberswap.com/explanation/core-libraries#outputs)

| Field            | Type      | Explanation                                                                                              |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| `usedAmount`     | `int256`  | actual amount to be used for the swap. >= 0 if `isExactInput` = true, <= 0 if `isExactInput` = false     |
| `returnedAmount` | `int256`  | output qty (<= 0) to be accumulated if `isExactInput` = true, input qty (>= 0) if `isExactInput` = false |
| `deltaL`         | `uint256` | collected swap fee, to be incremented to reinvest liquidity                                              |
| `nextSqrtP`      | `uint160` | new sqrt price after the computed swap step                                                              |

**Note**[**​**](https://docs.kyberswap.com/explanation/core-libraries#note)

`nextSqrtP` should not exceed `targetSqrtP`.

### `calcReachAmount()`[​](https://docs.kyberswap.com/explanation/core-libraries#calcreachamount) <a href="#calcreachamount" id="calcreachamount"></a>

Calculates the amount needed to reach `targetSqrtP` from `currentSqrtP`. Note that `currentSqrtP` and `targetSqrtP` are casted from uint160 to uint256 as they are multiplied by `TWO_BPS (20_000)` or `feeInBps`.

The mathematical formulas are provided below for reference.&#x20;

<table><thead><tr><th width="192">isExactInput</th><th width="184.33333333333331">isToken0</th><th>Formula</th></tr></thead><tbody><tr><td><code>true</code></td><td><code>true</code></td><td> <span class="math">\frac{2*BPS*L(\sqrt{p_c} - \sqrt{p_n})}{\sqrt{p_c}(2*BPS*\sqrt{p_n} - fee\sqrt{p_c})}</span> (>0)</td></tr><tr><td><code>true</code></td><td><code>false</code></td><td>  <span class="math">\frac{2*BPS*\sqrt{p_c}*L(\sqrt{p_n} - \sqrt{p_c})}{(2*BPS*\sqrt{p_c} - fee\sqrt{p_n})}</span> (>0) </td></tr><tr><td><code>false</code></td><td><code>true</code></td><td> <span class="math">-\frac{2*BPS*L(\sqrt{p_n} - \sqrt{p_c})}{\sqrt{p_c}(2*BPS*\sqrt{p_n} - fee\sqrt{p_c})}</span> (&#x3C;0)</td></tr><tr><td><code>false</code></td><td><code>false</code></td><td>  <span class="math">-\frac{2*BPS*\sqrt{p_c}*L(\sqrt{p_c} - \sqrt{p_n})}{(2*BPS*\sqrt{p_c} - fee\sqrt{p_n})}</span> (&#x3C;0)</td></tr></tbody></table>

Note that while cases 1 and 3 and cases 2 and 4 are mathematically equivalent, the implementation differs by performing a double negation for the exact output cases. It takes the difference of $$\sqrt{p_n}$$ and $$\sqrt{p_c}$$ in the numerator (>0), then performing a second negation.

| Input Field    | Type      | Formula Variable | Explanation                                                                        |
| -------------- | --------- | ---------------- | ---------------------------------------------------------------------------------- |
| `liquidity`    | `uint256` | $$L$$            | active base liquidity + reinvestment liquidity                                     |
| `currentSqrtP` | `uint160` | $$\sqrt{p_c}$$   | current sqrt price                                                                 |
| `targetSqrtP`  | `uint160` | $$\sqrt{p_n}$$   | sqrt price limit `nextSqrtP` can take                                              |
| `feeInBps`     | `uint256` | $$fee$$          | swap fee in basis points                                                           |
| `isExactInput` | `bool`    | N.A.             | true / false if specified swap amount refers to input / output amount respectively |
| `isToken0`     | `bool`    | N.A.             | true / false if specified swap amount is in token0 / token1 respectively           |

### `estimateIncrementalLiquidity()`[​](https://docs.kyberswap.com/explanation/core-libraries#estimateincrementalliquidity) <a href="#estimateincrementalliquidity" id="estimateincrementalliquidity"></a>

Estimates `deltaL`, the swap fee to be collected based on amountSpecified. This is called only for the final swap step, where the next (temporary) tick will not be crossed.

In the case where exact input is specified, the formula is rather straightforward.&#x20;

<table><thead><tr><th width="185">isToken0</th><th>Formula</th></tr></thead><tbody><tr><td><code>true</code></td><td><span class="math">\frac{delta*fee*\sqrt{p_c}}{2*BPS}</span> </td></tr><tr><td><code>false</code></td><td><span class="math">\frac{delta*fee}{2*BPS*\sqrt{p_c}}</span> </td></tr></tbody></table>

In the case where exact output is specified, a quadratic equation has to be solved. The desired result is the smaller root of the quadratic equation.

<table><thead><tr><th width="182">isToken0</th><th>Formula</th></tr></thead><tbody><tr><td><code>true</code></td><td><span class="math">fee*(\Delta{L})^2-2[(BPS-fee)*L-BPS*delta*\sqrt{p_c}]\Delta{L}+fee*L*delta*\sqrt{p_c}=0</span></td></tr><tr><td><code>false</code></td><td><span class="math">fee*(\Delta{L})^2-2[(BPS-fee)*L-\frac{BPS*delta}{\sqrt{p_c}}]\Delta{L}+\frac{fee*L*delta}{\sqrt{p_c}}=0</span></td></tr></tbody></table>

<table><thead><tr><th width="190">Input Field</th><th width="126">Type</th><th>Formula Variable</th><th>Explanation</th></tr></thead><tbody><tr><td><code>absDelta</code></td><td><code>uint256</code></td><td><span class="math">delta</span></td><td><span class="math">∥∥</span><code>usedAmount</code><span class="math">∥∥</span>, absolute value of <code>usedAmount</code> (actual amount used for swap)</td></tr><tr><td><code>liquidity</code></td><td><code>uint256</code></td><td><span class="math">L</span></td><td>active base liquidity + reinvestment liquidity</td></tr><tr><td><code>currentSqrtP</code></td><td><code>uint160</code></td><td><span class="math">\sqrt{p_c}</span></td><td>current sqrt price</td></tr><tr><td><code>feeInBps</code></td><td><code>uint256</code></td><td><span class="math">fee</span></td><td>swap fee in basis points</td></tr><tr><td><code>isExactInput</code></td><td><code>bool</code></td><td>N.A.</td><td>true / false if specified swap amount refers to input / output amount respectively</td></tr><tr><td><code>isToken0</code></td><td><code>bool</code></td><td>N.A.</td><td>true / false if specified swap amount is in token0 / token1 respectively</td></tr></tbody></table>

### `calcIncrementalLiquidity()`[​](https://docs.kyberswap.com/explanation/core-libraries#calcincrementalliquidity) <a href="#calcincrementalliquidity" id="calcincrementalliquidity"></a>

Calculates `deltaL`, the swap fee to be collected based on amountSpecified. This is called for an intermediate swap step, where the next (temporary) tick will be crossed.

The mathematical formulas are provided below for reference.&#x20;

<table><thead><tr><th width="192">isExactInput</th><th width="184.33333333333331">isToken0</th><th>Formula</th></tr></thead><tbody><tr><td><code>true</code></td><td><code>true</code></td><td> <span class="math">\sqrt{p_n}*(\frac{L}{\sqrt{p_c}}+\|delta\|)-L</span> </td></tr><tr><td><code>true</code></td><td><code>false</code></td><td> <span class="math">\frac{(L*\sqrt{p_c})+\|delta\|}{\sqrt{p_n}}-L</span> </td></tr><tr><td><code>false</code></td><td><code>true</code></td><td><span class="math">\sqrt{p_n}*(\frac{L}{\sqrt{p_c}}-\|delta\|)-L</span> </td></tr><tr><td><code>false</code></td><td><code>false</code></td><td> <span class="math">\frac{(L*\sqrt{p_c})-\|delta\|}{\sqrt{p_n}}-L</span> </td></tr></tbody></table>

**Inputs**

<table><thead><tr><th width="190">Input Field</th><th width="149">Type</th><th width="178">Formula Variable</th><th>Explanation</th></tr></thead><tbody><tr><td><code>absDelta</code></td><td><code>uint256</code></td><td>|<span class="math">delta</span>|</td><td><span class="math">∥∥</span><code>usedAmount</code><span class="math">∥∥</span>, absolute value of <code>usedAmount</code> (actual amount used for swap)</td></tr><tr><td><code>liquidity</code></td><td><code>uint256</code></td><td><span class="math">L</span></td><td>active base liquidity + reinvestment liquidity</td></tr><tr><td><code>currentSqrtP</code></td><td><code>uint160</code></td><td><span class="math">\sqrt{p_c}</span></td><td>current sqrt price</td></tr><tr><td><code>nextSqrtP</code></td><td><code>uint160</code></td><td><span class="math">\sqrt{p_n}</span></td><td>next sqrt price</td></tr><tr><td><code>isExactInput</code></td><td><code>bool</code></td><td>N.A.</td><td>true / false if specified swap amount refers to input / output amount respectively</td></tr><tr><td><code>isToken0</code></td><td><code>bool</code></td><td>N.A.</td><td>true / false if specified swap amount is in token0 / token1 respectively</td></tr></tbody></table>

### `calcFinalPrice()`[​](https://docs.kyberswap.com/explanation/core-libraries#calcfinalprice) <a href="#calcfinalprice" id="calcfinalprice"></a>

Calculates the sqrt price of the final swap step where the next (temporary) tick will not be crossed.

The mathematical formulas are provided below for reference.&#x20;

<table><thead><tr><th width="192">isExactInput</th><th width="184.33333333333331">isToken0</th><th>Formula</th></tr></thead><tbody><tr><td><code>true</code></td><td><code>true</code></td><td> <span class="math">\frac{(L+\Delta{L})\sqrt{p_c}}{L+\|delta\|\sqrt{p_c}}</span> </td></tr><tr><td><code>true</code></td><td><code>false</code></td><td> <span class="math">\frac{L\sqrt{p_c}+\|delta\|}{L+\Delta{L}}</span> </td></tr><tr><td><code>false</code></td><td><code>true</code></td><td><span class="math">\frac{(L+\Delta{L})\sqrt{p_c}}{L-\|delta\|\sqrt{p_c}}</span> </td></tr><tr><td><code>false</code></td><td><code>false</code></td><td> <span class="math">\frac{L\sqrt{p_c}-\|delta\|}{L+\Delta{L}}</span> </td></tr></tbody></table>

**Input**

| Input Field    | Type      | Formula Variable | Explanation                                                                            |
| -------------- | --------- | ---------------- | -------------------------------------------------------------------------------------- |
| `absDelta`     | `uint256` | \|$$delta$$\|    | $$∥∥$$`usedAmount`$$∥∥$$, absolute value of `usedAmount` (actual amount used for swap) |
| `liquidity`    | `uint256` | $$L$$            | active base liquidity + reinvestment liquidity                                         |
| `deltaL`       | `uint256` | $$ΔL$$           | collected swap fee                                                                     |
| `currentSqrtP` | `uint160` | $$\sqrt{p_c}$$   | current sqrt price                                                                     |
| `isExactInput` | `bool`    | N.A.             | true / false if specified swap amount refers to input / output amount respectively     |
| `isToken0`     | `bool`    | N.A.             | true / false if specified swap amount is in token0 / token1 respectively               |

### `calcReturnedAmount()`[​](https://docs.kyberswap.com/explanation/core-libraries#calcreturnedamount) <a href="#calcreturnedamount" id="calcreturnedamount"></a>

Calculates `returnedAmount` for the [`computeSwapStep`](elastic-core-libraries.md#computeswapstep) function. Rounds down when `isExactInput = true` (calculating output < 0) so that we avoid sending too much. Conversely, rounds up when `isExactInput = false` to ensure sufficient input > 0 will be received.

The mathematical formulas are provided below for reference.

**`isToken0 = true`**[**​**](https://docs.kyberswap.com/explanation/core-libraries#istoken0--true)

The formula is actually the same, with the difference being made to the operands to ensure the price difference is non-negative.

| isExactInput | Formula                                          |
| ------------ | ------------------------------------------------ |
| `true`       | $$\Delta{L}\sqrt{p_n}-L(\sqrt{p_c}-\sqrt{p_n})$$ |
| `false`      | $$\Delta{L}\sqrt{p_n}+L(\sqrt{p_n}-\sqrt{p_c})$$ |

**`isToken0 = false`**[**​**](https://docs.kyberswap.com/explanation/core-libraries#istoken0--false)

$$\frac{L+\Delta{L}}{\sqrt{p_n}} - \frac{L}{\sqrt{p_c}}$$

<table><thead><tr><th width="198">Input Field</th><th width="157">Type</th><th width="168">Formula Variable</th><th>Explanation</th></tr></thead><tbody><tr><td><code>liquidity</code></td><td><code>uint256</code></td><td><span class="math">L</span></td><td>active base liquidity + reinvestment liquidity</td></tr><tr><td><code>currentSqrtP</code></td><td><code>uint160</code></td><td><span class="math">\sqrt{p_c}</span></td><td>current sqrt price</td></tr><tr><td><code>nextSqrtP</code></td><td><code>uint160</code></td><td><span class="math">\sqrt{p_n}</span></td><td>next sqrt price</td></tr><tr><td><code>deltaL</code></td><td><code>uint256</code></td><td><span class="math">ΔL</span></td><td>collected swap fee</td></tr><tr><td><code>isExactInput</code></td><td><code>bool</code></td><td>N.A.</td><td>true / false if specified swap amount refers to input / output amount respectively</td></tr><tr><td><code>isToken0</code></td><td><code>bool</code></td><td>N.A.</td><td>true / false if specified swap amount is in token0 / token1 respectively</td></tr></tbody></table>

## TickMath[​](https://docs.kyberswap.com/explanation/core-libraries#tickmath) <a href="#tickmath" id="tickmath"></a>

Contains functions for computing square root prices from ticks and vice versa. Adapted from [Uniswap V3's TickMath library](https://github.com/Uniswap/v3-core/blob/main/contracts/libraries/TickMath.sol).

### Constants[​](https://docs.kyberswap.com/explanation/core-libraries#constants) <a href="#constants" id="constants"></a>

<table><thead><tr><th>Field</th><th width="154">Type</th><th>Value</th><th>Explanation</th></tr></thead><tbody><tr><td><code>MIN_TICK</code></td><td><code>int24</code></td><td><code>-887272</code></td><td>Minimum possible tick = <span class="math">{log_{1.0001}2^{-128}}</span></td></tr><tr><td><code>MAX_TICK</code></td><td><code>int24</code></td><td><code>887272</code></td><td>Minimum possible tick = <span class="math">{log_{1.0001}2^{128}}</span></td></tr><tr><td><code>MIN_SQRT_RATIO</code></td><td><code>uint160</code></td><td><code>4295128739</code></td><td><code>getSqrtRatioAtTick(MIN_TICK)</code></td></tr><tr><td><code>MAX_SQRT_RATIO</code></td><td><code>uint160</code></td><td><code>1461446703485210103287273052203988822378723970342</code></td><td><code>getSqrtRatioAtTick(MAX_TICK)</code></td></tr></tbody></table>

### `getSqrtRatioAtTick()`[​](https://docs.kyberswap.com/explanation/core-libraries#getsqrtratioattick) <a href="#getsqrtratioattick" id="getsqrtratioattick"></a>

Given a `int24 tick`, calculates $${\sqrt{1.0001^{tick}} * 2^{96}}$$.

### `getTickAtSqrtRatio()`[​](https://docs.kyberswap.com/explanation/core-libraries#gettickatsqrtratio) <a href="#gettickatsqrtratio" id="gettickatsqrtratio"></a>

Given a square root price ratio `uint160 sqrtP`, calculates the greatest `tick` such that `getSqrtRatioAtTick(tick) <= sqrtP`.

Note that `MIN_SQRT_RATIO <= sqrtP <= MAX_SQRT_RATIO`, otherwise the function will revert.

### `getMaxNumberTicks()`[​](https://docs.kyberswap.com/explanation/core-libraries#getmaxnumberticks) <a href="#getmaxnumberticks" id="getmaxnumberticks"></a>

Used to calculate the maximum liquidity allowable per tick. This function calculates the maximum number of ticks that can be inserted into the LinkedList, given a `tickDistance`.

| Field           | Type    | Explanation                                               |
| --------------- | ------- | --------------------------------------------------------- |
| `_tickDistance` | `int24` | Ticks can only be initialized at multiples of this value. |
