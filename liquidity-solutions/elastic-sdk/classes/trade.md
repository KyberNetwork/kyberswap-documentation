# Trade

{% hint style="info" %}
Represents a trade where a proportion of the trade can be routed via similar pair pools which consist of the input and output token. A Trade instance is created on the assumption that trade simulation has been correctly carried out elsewhere.



**GitHub File:** [trade.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/entities/trade.ts)
{% endhint %}

## Extends

* [Currency](https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4)
* [TradeType](https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L6)

## Properties

### Public

<table><thead><tr><th width="136">Property</th><th width="129">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>swaps</td><td>{}[]</td><td>readonly</td><td>Array of objects, each representing a swap that makes up the trade. Each swap contains:<br><br><code>route:</code> <a href="route.md"><code>Route</code></a><code>&#x3C;TInput, TOutput></code>  = The swap route.<br><br><code>inputAmount:</code> <a href="../../core-sdk/classes/currencyamount.md"><code>CurrencyAmount</code></a> = The input token for the swap.<br><br><code>outputAmount:</code> <a href="../../core-sdk/classes/currencyamount.md"><code>CurrencyAmount</code></a> = The output token for the swap. </td></tr><tr><td>tradeType</td><td>TTradeType</td><td>readonly</td><td>The type of trade: exact in OR exact out.</td></tr><tr><td>input</td><td>TInput</td><td>readonly</td><td>The input token for the swap.</td></tr><tr><td>output</td><td>TOutput</td><td>readonly</td><td>The output token for the swap.</td></tr></tbody></table>

### Private

<table><thead><tr><th width="178">Property</th><th width="244">Type</th><th>Description</th></tr></thead><tbody><tr><td>_inputAmount</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TInput></td><td>The cached result of the input amount computation.</td></tr><tr><td>_outputAmount</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TOutput></td><td>The cached result of the output amount computation.</td></tr><tr><td>_executionPrice</td><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;TInput, TOutput></td><td>The cached result of the computed execution price.</td></tr><tr><td>_priceImpact</td><td><a href="../../core-sdk/classes/percent.md">Percent</a> | undefined</td><td>The cached result of the price impact calculation.</td></tr></tbody></table>

## Constructor

The Trade class implements a private constructor whose validation logic is enforced via the [`createUncheckedTrade()`](trade.md#createuncheckedtrade-public-static) static factory method.

### Parameters

<table><thead><tr><th width="131">Params</th><th width="130">Type</th><th>Description</th></tr></thead><tbody><tr><td>{}</td><td>object</td><td>An object consisting of:<br><br><code>routes: {}[]</code> = Array of swaps which makes up the trade.<br><br><code>tradeType: TTradeType</code> = The type of trade: exact in OR exact out.</td></tr><tr><td>tradeType</td><td>TTradeType</td><td>The type of trade: exact in OR exact out.</td></tr></tbody></table>

## Methods

### createUncheckedTrade() - `public` `static`

Creates a Trade instance with a single hop. Does not validate the result of swapping through the route and is meant to be used when trade simulation has been done elsewhere.&#x20;

#### Parameters

<table><thead><tr><th width="221">Params</th><th width="72">Type</th><th>Description</th></tr></thead><tbody><tr><td>constructorArguments</td><td>{}</td><td>An object representing a single swap:<br><br><code>route:</code> <a href="route.md"><code>Route</code></a><code>&#x3C;TInput, TOutput></code>  = The swap route.<br><br><code>inputAmount:</code> <a href="../../core-sdk/classes/currencyamount.md"><code>CurrencyAmount</code></a> = The input token for the swap.<br><br><code>outputAmount:</code> <a href="../../core-sdk/classes/currencyamount.md"><code>CurrencyAmount</code></a> = The output token for the swap. <br><br><code>tradeType: TTradeType</code> = The type of trade: exact in OR exact out</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="336">Type</th><th>Description</th></tr></thead><tbody><tr><td>Trade&#x3C;TInput, TOutput, TTradeType></td><td>A new Trade instance consisting of the single hop unchecked trade.</td></tr></tbody></table>

***

### inputAmount() - `public` `get`

Returns the mid price of the route.

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;TInput, TOutput></td><td>The mid price of the route.</td></tr></tbody></table>

***

### inputAmount() - `public` `get`

Returns the amount of input tokens for the trade assuming no slippage.

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TInput></td><td>The amount of input token for the trade.</td></tr></tbody></table>

***

### outputAmount() - `public` `get`

Returns the amount of output tokens resulting from the trade assuming no slippage.

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TOutput></td><td>The amount of output tokens for the trade assuming no slippage.</td></tr></tbody></table>

***

### executionPrice() - `public` `get`

The price which the trade is executed at denoted in $$\frac{outputAmount}{inputAmount}$$.

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;TInput, TOutput></td><td>The execution price of the trade.</td></tr></tbody></table>

***

### priceImpact() - `public` `get`

Returns the percentage price difference between the route's mid price and the executed price (i.e. the price impact).

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td>Percent</td><td>The price impact denoted in % of the executed price.</td></tr></tbody></table>

***

### minimumAmountOut() - `public`

Given a slippage tolerance value, returns the minimum amount of output tokens resulting from this trade.

#### Parameters

<table><thead><tr><th width="202">Params</th><th width="164">Type</th><th>Description</th></tr></thead><tbody><tr><td>slippageTolerance</td><td><a href="../../core-sdk/classes/percent.md">Percent</a></td><td>The % amount that the final executed price can differ from the expected price before the transaction will revert.</td></tr><tr><td>amountOut</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TOutput></td><td>The amount of output tokens required for the trade. Used when trade type is exact out. Default is <code>this.amountOut</code>.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TOutput></td><td>The minimum amount of output tokens for the trade.</td></tr></tbody></table>

***

### maximumAmountIn() - `public`

Given a slippage tolerance value, returns the maximum amount of input tokens that the trade requires to be executed successfully.

#### Parameters

<table><thead><tr><th width="193">Params</th><th width="164">Type</th><th>Description</th></tr></thead><tbody><tr><td>slippageTolerance</td><td><a href="../../core-sdk/classes/percent.md">Percent</a></td><td>The % amount that the final executed price can differ from the expected price before the transaction will revert.</td></tr><tr><td>amountIn</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TOutput></td><td>The amount of input tokens for the trade. Used when trade type is exact in. Default is <code>this.amountIn</code>.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TOutput></td><td>The maximum amount of input tokens for the trade.</td></tr></tbody></table>

***

### worstExecutionPrice() - `public`

Given a slippage tolerance value, returns the worst price that the trade can be executed at.

#### Parameters

<table><thead><tr><th width="204">Params</th><th width="164">Type</th><th>Description</th></tr></thead><tbody><tr><td>slippageTolerance</td><td><a href="../../core-sdk/classes/percent.md">Percent</a></td><td>The % amount that the final executed price can differ from the expected price before the transaction will revert.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TOutput></td><td>The worst price that the trade can be executed at.</td></tr></tbody></table>
