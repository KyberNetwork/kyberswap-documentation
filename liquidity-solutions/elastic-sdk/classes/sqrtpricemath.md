# SqrtPriceMath

{% hint style="info" %}
Compute deltas based on liquidity and square root price data.



**GitHub File:** [sqrtPriceMath.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/utils/sqrtPriceMath.ts)
{% endhint %}

## Constructor

Private constructor that cannot be constructed.

## Methods

### getAmount0Unlock() - `public` `static`

Returns the amount of token0 required to initialize the pool.

#### Parameters

<table><thead><tr><th width="180">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioInitX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The square root price of the pool upon initialization, denominated in Q notation.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of token0 required to initialize the pool.</td></tr></tbody></table>

***

### getAmount1Unlock() - `public` `static`

Returns the amount of token1 required to initialize the pool.

#### Parameters

<table><thead><tr><th width="180">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioInitX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The square root price of the pool upon initialization, denominated in Q notation.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of token1 required to initialize the pool.</td></tr></tbody></table>

***

### getAmount0Delta() - `public` `static`

Gets the liquidity delta between two token0 prices.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioAX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>A sqrt price of token0.</td></tr><tr><td>sqrtRatioBX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Another sqrt price of token0.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>roundUp</td><td>boolean</td><td><code>true</code> = Result is rounded up to the nearest integer.<br><code>false</code> = Result is not rounded down to the ne</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Amount of token0 required to cover a position of size liquidity between the two passed prices.</td></tr></tbody></table>

***

### getAmount1Delta() - `public` `static`

Gets the liquidity delta between two token1 prices.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioAX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>A sqrt price of token0.</td></tr><tr><td>sqrtRatioBX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Another sqrt price of token0.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>roundUp</td><td>boolean</td><td><code>true</code> = Result is rounded up to the nearest integer.<br><code>false</code> = Result is not rounded down to the ne</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Amount of token1 required to cover a position of size liquidity between the two passed prices.</td></tr></tbody></table>

***

### getNextSqrtPriceFromInput() - `public` `static`

Gets the next sqrt price given an input amount of token0 or token1.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtPX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>A sqrt price of token0.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>amounIn</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of tokens being swapped in.</td></tr><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Amount in is in token1.<br><code>false</code> = Amount in is in token0.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The price after removing the output amount of token0 or token1</td></tr></tbody></table>

***

### getNextSqrtPriceFromOutput() - `public` `static`

Gets the next sqrt price given an output amount of token0 or token1.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtPX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>A sqrt price of token0.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>amountOut</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of tokens being swapped out.</td></tr><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Amount out is in token1.<br><code>false</code> = Amount out is in token0.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The price after removing the output amount of token0 or token1</td></tr></tbody></table>

***

### getNextSqrtPriceFromAmount0RoundingUp() - `private` `static`

Gets the next sqrt price given a delta of token0. The token0 price is rounded up to ensure that the virtual reserves never falls below `0` and the output amount is always achieved.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtPX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The starting price of of token0.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>amount</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of token0 to add or remove from virtual reserves.</td></tr><tr><td>add</td><td>boolean</td><td><code>true</code> = Amount is added to the virtual reserve.<br><code>false</code> = Amount is removed from the virtual reserve.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The token0 price after adding or removing the amount specified.</td></tr></tbody></table>

***

### getNextSqrtPriceFromAmount1RoundingDown() - `private` `static`

Gets the next sqrt price given a delta of token1. The token1 price is rounded down to ensure that the virtual reserves never falls below `0` and the output amount is always achieved.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtPX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The starting price of of token1.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>amount</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of token0 to add or remove from virtual reserves.</td></tr><tr><td>add</td><td>boolean</td><td><code>true</code> = Amount is added to the virtual reserve.<br><code>false</code> = Amount is removed from the virtual reserve.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The token1 price after adding or removing the amount specified.</td></tr></tbody></table>
