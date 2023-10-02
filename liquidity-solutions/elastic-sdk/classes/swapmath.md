# SwapMath

{% hint style="info" %}
Handles the swap maths within ticks.



**GitHub File:** [swapMath.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/utils/swapMath.ts)
{% endhint %}

## Constructor

Private constructor that cannot be constructed.

## Methods

### computeSwapStepPromm() - `public` `static`

Returns the price and token amounts resulting from an Elastic swap.

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="129">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioCurrentX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The current square root price of the pool denominated in Q notation.</td></tr><tr><td>sqrtRatioTargetX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The target square root price of the pool following the swap denominated in Q notation. Direction of the swap is inferred by comparing the target price against the current pool price.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>amountRemaining</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Remaining amount of tokens that needs to be swapped in or out.</td></tr><tr><td>feePips</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/constants.ts#L10">FeeAmount</a></td><td>The swap fee taken from the input amount, denominated in hundredths of bips.</td></tr><tr><td>exactIn</td><td>boolean</td><td><code>true</code> = Swap logic is based on exact in.<br><code>false</code> = Swap logic is based on exact out.</td></tr><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Swap is from token0 to token1.<br><code>false</code> = Swap is from token1 to token0.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="227">Type</th><th>Description</th></tr></thead><tbody><tr><td>[<a href="https://www.npmjs.com/package/jsbi">JSBI</a>, <a href="https://www.npmjs.com/package/jsbi">JSBI</a>, <a href="https://www.npmjs.com/package/jsbi">JSBI</a>, <a href="https://www.npmjs.com/package/jsbi">JSBI</a>]</td><td>An array consisting of the following value by index:<br><br><code>0</code> = The square root price after the swap.<br><br><code>1</code> = The amount of input tokens for the swap.<br><br><code>2</code> = The amount of output tokens from the swap.<br><br><code>3</code> = The liquidity delta due to the swap.</td></tr></tbody></table>

***

### calcReachAmount() - `public` `static`

Returns the amount of tokens used in the swap in order to reach the target price.

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="129">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioCurrentX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The current square root price of the pool denominated in Q notation.</td></tr><tr><td>sqrtRatioTargetX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The target square root price of the pool following the swap denominated in Q notation. Direction of the swap is inferred by comparing the target price against the current pool price.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>feePips</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/constants.ts#L10">FeeAmount</a></td><td>The swap fee taken from the input amount, denominated in hundredths of bips.</td></tr><tr><td>exactIn</td><td>boolean</td><td><code>true</code> = Swap logic is based on exact in.<br><code>false</code> = Swap logic is based on exact out.</td></tr><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Swap is from token0 to token1.<br><code>false</code> = Swap is from token1 to token0.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of tokens used in the swap in order to reach the target price.</td></tr></tbody></table>

***

### calcReturnedAmount() - `public` `static`

Returns the output token amount from the swap.

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="129">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioCurrentX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The current square root price of the pool denominated in Q notation.</td></tr><tr><td>sqrtRatioTargetX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The target square root price of the pool following the swap denominated in Q notation. Direction of the swap is inferred by comparing the target price against the current pool price.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>deltaL</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The liquidity delta due to the swap.</td></tr><tr><td>feePips</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/constants.ts#L10">FeeAmount</a></td><td>The swap fee taken from the input amount, denominated in hundredths of bips.</td></tr><tr><td>exactIn</td><td>boolean</td><td><code>true</code> = Swap logic is based on exact in.<br><code>false</code> = Swap logic is based on exact out.</td></tr><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Swap is from token0 to token1.<br><code>false</code> = Swap is from token1 to token0.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Swap output token amount.</td></tr></tbody></table>

***

### calcIncrementalLiquidity() - `public` `static`

Returns the incremental liquidity in the case where the resulting pool price after the swap is non-zero (i.e. target price was reached within the pool).

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="129">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioCurrentX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The current square root price of the pool denominated in Q notation.</td></tr><tr><td>sqrtRatioTargetX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The target square root price of the pool following the swap denominated in Q notation. Direction of the swap is inferred by comparing the target price against the current pool price.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>absAmount</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The absolute amount of tokens used for the swap.</td></tr><tr><td>exactIn</td><td>boolean</td><td><code>true</code> = Swap logic is based on exact in.<br><code>false</code> = Swap logic is based on exact out.</td></tr><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Swap is from token0 to token1.<br><code>false</code> = Swap is from token1 to token0.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The incremental liquidity amount following a swap.</td></tr></tbody></table>

***

### estimateIncrementalLiquidity() - `public` `static`

Returns the estimated incremental liquidity in the case where the resulting pool price after the swap is zero (i.e. target price is outside the pool).

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="129">Type</th><th>Description</th></tr></thead><tbody><tr><td>absAmount</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The absolute amount of tokens used for the swap.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>sqrtRatioCurrentX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The current square root price of the pool denominated in Q notation.</td></tr><tr><td>feePips</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/constants.ts#L10">FeeAmount</a></td><td>The swap fee taken from the input amount, denominated in hundredths of bips.</td></tr><tr><td>exactIn</td><td>boolean</td><td><code>true</code> = Swap logic is based on exact in.<br><code>false</code> = Swap logic is based on exact out.</td></tr><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Swap is from token0 to token1.<br><code>false</code> = Swap is from token1 to token0.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The estimated incremental liquidity amount following a swap.</td></tr></tbody></table>

***

### calcFinalPrice() - `public` `static`

Returns the final price following the swap.

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="129">Type</th><th>Description</th></tr></thead><tbody><tr><td>absAmount</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The absolute amount of tokens used for the swap.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of usable liquidity.</td></tr><tr><td>deltaL</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The liquidity delta due to the swap.</td></tr><tr><td>sqrtRatioCurrentX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The current square root price of the pool denominated in Q notation.</td></tr><tr><td>feePips</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/constants.ts#L10">FeeAmount</a></td><td>The swap fee taken from the input amount, denominated in hundredths of bips.</td></tr><tr><td>exactIn</td><td>boolean</td><td><code>true</code> = Swap logic is based on exact in.<br><code>false</code> = Swap logic is based on exact out.</td></tr><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Swap is from token0 to token1.<br><code>false</code> = Swap is from token1 to token0.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The final price following the swap.</td></tr></tbody></table>
