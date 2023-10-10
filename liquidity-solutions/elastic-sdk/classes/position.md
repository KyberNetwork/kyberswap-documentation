# Position

{% hint style="info" %}
Maintains information about a Position. Contains additional methods that aids in calculating liquidity and token amoutns for the purposes of creating or closing positions.



**GitHub File:** [position.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/entities/position.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="177">Property</th><th width="122">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>pool</td><td><a href="pool.md">Pool</a></td><td>readonly</td><td>The pool in which the position was created.</td></tr><tr><td>tickLower</td><td>number</td><td>readonly</td><td>The lower tick of the position. The position is out-of-range if the pool's active tick is below this.</td></tr><tr><td>tickUpper</td><td>number</td><td>readonly</td><td>The upper tick of the position. The position is out-of-range if the pool's active tick is above this.</td></tr><tr><td>liquidity</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>The current value of in-range <a href="../../kyberswap-elastic/concepts/concentrated-liquidity.md#liquidity-tracking-lp-contributions-at-a-specific-price">liquidity</a>.</td></tr></tbody></table>

### Private

<table><thead><tr><th width="175">Property</th><th width="230">Type</th><th>Description</th></tr></thead><tbody><tr><td>_token0Amount</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>> | null</td><td>The position's token0 amount. Default is <code>null</code>.</td></tr><tr><td>_token1Amount</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>> | null</td><td>The position's token1 amount. Default is <code>null</code>.</td></tr><tr><td>_mintAmounts</td><td>Readonly&#x3C;{ amount0: <a href="https://www.npmjs.com/package/jsbi">JSBI</a>; amount1: <a href="https://www.npmjs.com/package/jsbi">JSBI</a> }> | null</td><td>The amount of liquidity held by the position at the current price of the pool.</td></tr></tbody></table>

## Constructor

### Parameters

<table><thead><tr><th width="131">Params</th><th width="218">Type</th><th>Description</th></tr></thead><tbody><tr><td>{}</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/entities/position.ts#L12">PositionConstructorArgs</a></td><td>An object that that contains the following:<br><br><code>pool</code> = The pool in which the position was created.<br><br><code>tickLower</code> = The lower tick of the position.<br><br><code>tickUpper</code> = The upper tick of the position.<br><br><code>liquidity</code> = The current value of in-range liquidity.</td></tr></tbody></table>

## Methods

### token0PriceLower() - `public` `get`

Returns the price of token0 at the position's lower tick quoted in terms of token1.

#### Returns

<table><thead><tr><th width="236">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>, <a href="../../core-sdk/classes/token.md">Token</a>></td><td>Price of token0 at the lower tick.</td></tr></tbody></table>

***

### token0PriceUpper() - `public` `get`

Returns the price of token0 at the position's upper tick quoted in terms of token1.

#### Returns

<table><thead><tr><th width="236">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>, <a href="../../core-sdk/classes/token.md">Token</a>></td><td>Price of token0 at the upper tick.</td></tr></tbody></table>

***

### amount0() - `public` `get`

Returns the position's token0 balance at the current price. This is the token0 amount that can be withdrawn if the NFT representing the position is burned.

#### Returns

<table><thead><tr><th width="276">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>></td><td>The position's token0 balance at the current price. Denominated in the token0 currency format.</td></tr></tbody></table>

***

### amount1() - `public` `get`

Returns the position's token1 balance at the current price. This is the token1 amount that can be withdrawn if the NFT representing the position is burned.

#### Returns

<table><thead><tr><th width="276">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;<a href="../../core-sdk/classes/token.md">Token</a>></td><td>The position's token1 balance at the current price. Denominated in the token1 currency format.</td></tr></tbody></table>

***

### ratiosAfterSlippage() - `private`

Returns the lower and upper price boundaries given a slippage tolerance percentage value.

#### Parameters

<table><thead><tr><th width="196">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>slippageTolerance</td><td><a href="../../core-sdk/classes/percent.md">Percent</a></td><td>The % amount that the final executed price can differ from the expected price before the transaction will revert.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="128">Type</th><th>Description</th></tr></thead><tbody><tr><td>{}</td><td>Object that consists of the lower and upper bounds for the transaction denoted in <a href="https://en.wikipedia.org/wiki/Q_(number_format)">Q notation format</a> to maximize gas efficiency:<br><br><code>sqrtRatioX96Lower:</code><a href="https://www.npmjs.com/package/jsbi"><code>JSBI</code></a> = The lowest price for the trade below which the transaction will fail. <br><br><code>sqrtRatioX96Upper:</code><a href="https://www.npmjs.com/package/jsbi"><code>JSBI</code></a> = The highest price for the trade below which the transaction will fail.<br><br><br><span class="math">price = (\frac{sqrtRatioX96}{2^{96}})^2</span> </td></tr></tbody></table>

***

### mintAmountsWithSlippage() - `public`

Given a slippage tolerance percentage value, returns the minimum amount of each pool token that is required for the position to be safely created (i.e. mint the position NFT).

#### Parameters

<table><thead><tr><th width="196">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>slippageTolerance</td><td><a href="../../core-sdk/classes/percent.md">Percent</a></td><td>The % amount that the final executed price can differ from the expected price before the transaction will revert.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="161">Type</th><th>Description</th></tr></thead><tbody><tr><td>ReadOnly&#x3C;{}></td><td>A read only object that consists of:<br><br><code>amount0:</code><a href="https://www.npmjs.com/package/jsbi"><code>JSBI</code></a> = The token0 amount required to safely create the position given a slippage tolerance percentage.<br><br><code>amount1:</code><a href="https://www.npmjs.com/package/jsbi"><code>JSBI</code></a> = The token1 amount required to safely create the position given a slippage tolerance percentage.</td></tr></tbody></table>

***

### burnAmountsWithSlippage() - `public`

Given a slippage tolerance percentage value, returns the minimum amount of each pool token that can be safely returned when the position is closed (i.e. burn the position NFT).

#### Parameters

<table><thead><tr><th width="196">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>slippageTolerance</td><td><a href="../../core-sdk/classes/percent.md">Percent</a></td><td>The % amount that the final executed price can differ from the expected price before the transaction will revert.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="161">Type</th><th>Description</th></tr></thead><tbody><tr><td>ReadOnly&#x3C;{}></td><td>A read only object that consists of:<br><br><code>amount0:</code><a href="https://www.npmjs.com/package/jsbi"><code>JSBI</code></a> = The token0 amount that can be safely returned when the position is closed given a slippage tolerance percentage.<br><br><code>amount1:</code><a href="https://www.npmjs.com/package/jsbi"><code>JSBI</code></a> = The token1 amount that can be safely returned when the position is closed given a slippage tolerance percentage.</td></tr></tbody></table>

***

### mintAmounts() - `public` `get`

Returns the minimum amount of each pool token that is required for the position to be safely created (i.e. mint the position NFT).

#### Returns

<table><thead><tr><th width="161">Type</th><th>Description</th></tr></thead><tbody><tr><td>ReadOnly&#x3C;{}></td><td>A read only object that consists of:<br><br><code>amount0:</code><a href="https://www.npmjs.com/package/jsbi"><code>JSBI</code></a> = The token0 amount required to safely create the position.<br><br><code>amount1:</code><a href="https://www.npmjs.com/package/jsbi"><code>JSBI</code></a> = The token1 amount required to safely create the position.</td></tr></tbody></table>

***

### fromAmounts() - `public` `static`

Given both token amounts and the position's tick range, calculates the maximum liquidity for the position being created. The result is returned as a new Position instance.&#x20;

#### Parameters

<table><thead><tr><th width="107">Params</th><th width="81">Type</th><th>Description</th></tr></thead><tbody><tr><td>{}</td><td>object</td><td>An object consisting of:<br><br><code>pool:</code><a href="pool.md"><code>Pool</code></a> = The pool on which to create the position.<br><br><code>tickLower: number</code> = The lower tick of the position to be created.<br><br><code>tickUpper: number</code> =The upper tick of the position to be created.<br><br><code>amount0:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = The token0 amount that is being provided.<br><br><code>amount1:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = The token1 amount that is being provided.<br><br><code>useFullPrecision: boolean</code> = <code>true</code> -> Calculates theoretical max liquidity; <code>false</code> -> Calculates max liquidity according to what the router can support</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="161">Type</th><th>Description</th></tr></thead><tbody><tr><td>Position</td><td>A new Position instance which consists of the max liquidity value.</td></tr></tbody></table>

***

### fromAmount0() - `public` `static`

Given a token0 amount and the position's tick range, calculates the maximum liquidity for the position being created. Assumes an unlimited amount of token1. The result is returned as a new Position instance.&#x20;

#### Parameters

<table><thead><tr><th width="107">Params</th><th width="81">Type</th><th>Description</th></tr></thead><tbody><tr><td>{}</td><td>object</td><td>An object consisting of:<br><br><code>pool:</code><a href="pool.md"><code>Pool</code></a> = The pool on which to create the position.<br><br><code>tickLower: number</code> = The lower tick of the position to be created.<br><br><code>tickUpper: number</code> =The upper tick of the position to be created.<br><br><code>amount0:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = The token0 amount that is being provided.<br><br><code>useFullPrecision: boolean</code> = <code>true</code> -> Calculates theoretical max liquidity; <code>false</code> -> Calculates max liquidity according to what the router can support</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="161">Type</th><th>Description</th></tr></thead><tbody><tr><td>Position</td><td>A new Position instance which consists of the max liquidity value.</td></tr></tbody></table>

***

### fromAmount1() - `public` `static`

Given a token1 amount and the position's tick range, calculates the maximum liquidity for the position being created. Assumes an unlimited amount of token0. The result is returned as a new Position instance.&#x20;

Note that the function uses the full precision to calculate the liquidity amount.

#### Parameters

<table><thead><tr><th width="107">Params</th><th width="81">Type</th><th>Description</th></tr></thead><tbody><tr><td>{}</td><td>object</td><td>An object consisting of:<br><br><code>pool:</code><a href="pool.md"><code>Pool</code></a> = The pool on which to create the position.<br><br><code>tickLower: number</code> = The lower tick of the position to be created.<br><br><code>tickUpper: number</code> =The upper tick of the position to be created.<br><br><code>amount1:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = The token0 amount that is being provided.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="161">Type</th><th>Description</th></tr></thead><tbody><tr><td>Position</td><td>A new Position instance which consists of the max liquidity value.</td></tr></tbody></table>
