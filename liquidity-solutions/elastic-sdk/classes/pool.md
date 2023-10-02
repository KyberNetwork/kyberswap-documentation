# Pool

{% hint style="info" %}
Maintains information about the pool from creation and is constantly updated whenever a swap takes place against the pool.



**GitHub File:** [pool.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/entities/pool.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="177">Property</th><th width="122">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>token0</td><td><a href="../../core-sdk/classes/token.md">Token</a></td><td>readonly</td><td>Token0 of the pool.</td></tr><tr><td>token1</td><td><a href="../../core-sdk/classes/token.md">Token</a></td><td>readonly</td><td>Token1 of the pool.</td></tr><tr><td>fee</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/constants.ts#L10">FeeAmount</a></td><td>readonly</td><td>The fee tier (in bips) for the pool which determines the exact % trading fees that the pool charges.</td></tr><tr><td>sqrtRatioX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>The price quoted in token0:token1 and stored in <a href="https://en.wikipedia.org/wiki/Q_(number_format)">Q notation format</a> to maximize gas efficiency. <br><br><span class="math">price = (\frac{sqrtRatioX96}{2^{96}})^2</span></td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>The current value of in-range <a href="../../kyberswap-elastic/concepts/concentrated-liquidity.md#liquidity-tracking-lp-contributions-at-a-specific-price">liquidity</a>.</td></tr><tr><td>reinvestLiquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>The liquidity portion which has been reinvested into the <a href="../../kyberswap-elastic/concepts/reinvestment-curve.md">reinvestment curve</a>.</td></tr><tr><td>tickCurrent</td><td>number</td><td>readonly</td><td>The current <a href="../../kyberswap-elastic/concepts/tick-range-mechanism.md">tick</a> of the pool.</td></tr><tr><td>tickDataProvider</td><td>TickDataProvider</td><td>readonly</td><td>The data provider that can return tick data.</td></tr></tbody></table>

### Private

<table><thead><tr><th width="149">Property</th><th width="196">Type</th><th>Description</th></tr></thead><tbody><tr><td>_token0Price</td><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>, <a href="../../core-sdk/classes/token.md">Token</a>></td><td></td></tr><tr><td>_token1Price</td><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>, <a href="../../core-sdk/classes/token.md">Token</a>></td><td></td></tr></tbody></table>

## Constructor

<table><thead><tr><th width="177">Params</th><th width="181">Type</th><th>Description</th></tr></thead><tbody><tr><td>tokenA</td><td><a href="../../core-sdk/classes/token.md">Token</a></td><td>Token to use as Token0 of the pool.</td></tr><tr><td>tokenB</td><td><a href="../../core-sdk/classes/token.md">Token</a></td><td>Token to use as Token1 of the pool.</td></tr><tr><td>fee</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/constants.ts#L10">FeeAmount</a></td><td>The fee tier (in bips) for the pool which determines the exact % trading fees that the pool charges.</td></tr><tr><td>sqrtRatioX96</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The price quoted in token0:token1 and stored in <a href="https://en.wikipedia.org/wiki/Q_(number_format)">Q notation format</a> to maximize gas efficiency. <br><br><span class="math">price = (\frac{sqrtRatioX96}{2^{96}})^2</span></td></tr><tr><td>liquidity</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The current value of in-range <a href="../../kyberswap-elastic/concepts/concentrated-liquidity.md#liquidity-tracking-lp-contributions-at-a-specific-price">liquidity</a>.</td></tr><tr><td>reinvestLiquidity</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The liquidity portion which has been reinvested into the <a href="../../kyberswap-elastic/concepts/reinvestment-curve.md">reinvestment curve</a>.</td></tr><tr><td>tickCurrent</td><td>number</td><td>The current <a href="../../kyberswap-elastic/concepts/tick-range-mechanism.md">tick</a> of the pool.</td></tr><tr><td>tickDataProvider</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/entities/tickDataProvider.ts#L7">TickDataProvider</a> | (<a href="tick.md">Tick</a> | <a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/entities/tick.ts#L6">TickConstructorArgs</a>)[]</td><td>The current state of the pool ticks or a data provider that can return tick data.</td></tr></tbody></table>

## Methods

### involvesToken() - `public`

Returns true if the token passed in matches either token0 or token1 of the pool.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>token</td><td><a href="../../core-sdk/classes/token.md">Token</a></td><td>The token to check against the pool's tokens.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td><code>true</code> = The token matches either token0 or token1 of the pool.<br><code>false</code> = The token is not part of the pool.</td></tr></tbody></table>

***

### token0Price() - `public` `get`

Accessor that returns the current mid price of the pool in terms of token0. In other words, this function gets the ratio of $$\frac{token_1}{token_0}$$.

#### Returns

<table><thead><tr><th width="234">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/price.md">Price</a> &#x3C;<a href="../../core-sdk/classes/token.md">Token</a>, <a href="../../core-sdk/classes/token.md">Token</a>></td><td>The current mid price of the pool in terms of token0.</td></tr></tbody></table>

***

### token1Price() - `public` `get`

Accessor that returns the current mid price of the pool in terms of token1. In other words, this function gets the ratio of $$\frac{token_0}{token_1}$$.

#### Returns

<table><thead><tr><th width="234">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/price.md">Price</a> &#x3C;<a href="../../core-sdk/classes/token.md">Token</a>, <a href="../../core-sdk/classes/token.md">Token</a>></td><td>The current mid price of the pool in terms of token1.</td></tr></tbody></table>

***

### priceOf() - `public`

Returns the price of the given token in terms of the other token in the pool. That is, the price of token0 in terms of token1 if token0 is passed in and vice versa.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>token</td><td><a href="../../core-sdk/classes/token.md">Token</a></td><td>The token which to get the price.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="241">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/price.md">Price</a> &#x3C;<a href="../../core-sdk/classes/token.md">Token</a>, <a href="../../core-sdk/classes/token.md">Token</a>></td><td>The price of the given token in terms of the corresponding token in the pool.</td></tr></tbody></table>

***

### chainId() - `public` `get`

Accessor that returns the chainID of the tokens in pool (i.e. the chain which the tokens are deployed on).&#x20;

#### Returns

<table><thead><tr><th width="130">Type</th><th>Description</th></tr></thead><tbody><tr><td>number</td><td>The chainID of the underlying chain which the pools' tokens are deployed on.</td></tr></tbody></table>

***

### getOutputAmount() - `public` `async`

Returns the other token output amount given an input amount of one of the pool's tokens. The updated pool state following the trade is also returned.

#### Parameters

<table><thead><tr><th width="186">Params</th><th width="235">Type</th><th>Description</th></tr></thead><tbody><tr><td>inputAmount</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>></td><td>The amount of input tokens to be traded.</td></tr><tr><td>sqrtPriceLimitX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The price limit for the swap. If swapping from token0 to token1, the price cannot be less than this value after the swap and vice versa.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="255">Type</th><th>Description</th></tr></thead><tbody><tr><td>Promise&#x3C;[<a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>>, <a href="pool.md">Pool</a>]></td><td>A promise array whose index consists of:<br><code>0</code> = A quote of the raw amount of the other token that will result from this trade.<br><code>1</code> = The updated pool state following the trade.</td></tr></tbody></table>

***

### getOutputAmountProMM() - `public` `async`

Returns the other token output amount given an input amount of one of the pool's tokens. The updated pool state following the trade is also returned which includes the base and reinvestment liquidity.

#### Parameters

<table><thead><tr><th width="186">Params</th><th width="235">Type</th><th>Description</th></tr></thead><tbody><tr><td>inputAmount</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>></td><td>The amount of input tokens to be traded.</td></tr><tr><td>sqrtPriceLimitX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The price limit for the swap. If swapping from token0 to token1, the price cannot be less than this value after the swap and vice versa.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="255">Type</th><th>Description</th></tr></thead><tbody><tr><td>Promise&#x3C;[<a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>>, <a href="pool.md">Pool</a>]></td><td>A promise array whose index consists of:<br><code>0</code> = The raw amount of the other token that will result from this trade.<br><code>1</code> = The updated pool state following the trade which includes Elastic's base and reinvestment liquidity.</td></tr></tbody></table>

***

### swapProMM() - `private` `async`

Replicates the smart contract tick math in order to calculate the swap output and pool state changes following a swap. This function is similar to `swap()` but also calculates the base and reinvestment liquidity following an Elastic swap.

#### Parameters

<table><thead><tr><th width="186">Params</th><th width="235">Type</th><th>Description</th></tr></thead><tbody><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Swap is for token0 -> token1<br><code>false</code> = Swap is for token1 -> token0</td></tr><tr><td>amountSpecified</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of input tokens to be traded.</td></tr><tr><td>sqrtPriceLimitX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The price limit for the swap. If swapping from token0 to token1, the price cannot be less than this value after the swap and vice versa.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="255">Type</th><th>Description</th></tr></thead><tbody><tr><td>Promise&#x3C;{ amountCalculated: JSBI; sqrtRatioX96: JSBI; liquidity: JSBI; tickCurrent: number }></td><td>A promise object which consists of:<br><br><code>amountCalculated</code> = The raw amount of the other token that will result from this trade.<br><br><code>sqrtRatioX96</code> = The resulting price of the pool following the trade.<br><br><code>baseL</code> = The base liquidity value of the pool following the trade.<br><br><code>reinvestL</code> = The reinvest liquidity value of the pool following the trade.<br><br><code>tickCurrent</code> = The active tick of the pool following the trade.</td></tr></tbody></table>

***

### swap() - `private` `async`

Replicates the smart contract tick math in order to calculate the swap output and pool state changes following a swap.

#### Parameters

<table><thead><tr><th width="186">Params</th><th width="235">Type</th><th>Description</th></tr></thead><tbody><tr><td>zeroForOne</td><td>boolean</td><td><code>true</code> = Swap is for token0 -> token1<br><code>false</code> = Swap is for token1 -> token0</td></tr><tr><td>amountSpecified</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The amount of input tokens to be traded.</td></tr><tr><td>sqrtPriceLimitX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The price limit for the swap. If swapping from token0 to token1, the price cannot be less than this value after the swap and vice versa.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="255">Type</th><th>Description</th></tr></thead><tbody><tr><td>Promise&#x3C;{ amountCalculated: JSBI; sqrtRatioX96: JSBI; liquidity: JSBI; tickCurrent: number }></td><td>A promise object which consists of:<br><br><code>amountCalculated</code> = The raw amount of the other token that will result from this trade.<br><br><code>sqrtRatioX96</code> = The resulting price of the pool following the trade.<br><br><code>liquidity</code> = The liquidity value of the pool following the trade.<br><br><code>tickCurrent</code> = The active tick of the pool following the trade.</td></tr></tbody></table>

***

### tickSpacing() - `public` `get`

Returns the tick spacing that corresponds to the pool's configured fee.

#### Returns

<table><thead><tr><th width="255">Type</th><th>Description</th></tr></thead><tbody><tr><td>number</td><td>The tick spacing of the pool.</td></tr></tbody></table>
