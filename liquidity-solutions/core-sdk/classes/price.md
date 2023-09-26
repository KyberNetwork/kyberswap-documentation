# Price

{% hint style="info" %}
Enables the safe handling of prices.



**GitHub File:** [price.ts](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/fractions/price.ts)
{% endhint %}

## Extends

* [Fraction](fraction.md)

## Properties

### Public

<table><thead><tr><th width="167">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>baseCurrency</td><td>TBase</td><td>readonly</td><td>The input currency (i.e. denominator) from which to construct the price.</td></tr><tr><td>quoteCurrency</td><td>TQoute</td><td>readonly</td><td>The output currency (i.e. numerator) to which the price is constructed.</td></tr><tr><td>scalar</td><td><a href="fraction.md">Fraction</a></td><td>readonly</td><td>Used to adjust the raw fraction with regards to the decimals of the base and quote Token.</td></tr></tbody></table>

## Constructor

#### Parameters

<table><thead><tr><th width="149">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>args</td><td>Object</td><td>An object containing either:<br>-  The array literally detailing the Currency classes and amounts; or <br>- A second array that contains the Currency details in the <a href="currencyamount.md">CurrencyAmount</a> instances</td></tr></tbody></table>

## Methods

### invert() - `public`&#x20;

Flips the base and quote currency to display the inverted price.

#### Returns

<table><thead><tr><th width="244">Type</th><th>Description</th></tr></thead><tbody><tr><td>Price&#x3C;TQuote, TBase></td><td>The inverted price of the Price instance.</td></tr></tbody></table>

***

### multiply() - `public`

Multiplies the Price instance with the provided price and returns a new price. The provided price must have the same base currency as the Price's quote currency.

#### Parameters

<table><thead><tr><th width="112">Params</th><th width="216">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Price&#x3C;TQuote, TBase></td><td>The price to be multiplied with the Price instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="308">Type</th><th>Description</th></tr></thead><tbody><tr><td>Price&#x3C;TBase, TOtherQuote></td><td>The final Price after multiplying the two prices.</td></tr></tbody></table>

***

### quote() - `public`

Returns the amount of quote currency corresponding to a given amount of the base currency. That is, what is the provided currency amount when quoted in currency corresponding to the Price instance.

#### Parameters

<table><thead><tr><th width="176">Params</th><th width="244">Type</th><th>Description</th></tr></thead><tbody><tr><td>currencyAmount</td><td>currencyAmount&#x3C;TBase></td><td>The base currency amount to convert.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="260">Type</th><th>Description</th></tr></thead><tbody><tr><td>CurrencyAmount&#x3C;TQuote></td><td>The amount of quote currency equivalent to the given base currency amount.</td></tr></tbody></table>

***

### adjustedForDecimals() - `private`

Scale the Price value by the `scalar` amount to prepare the price for further formatting

#### Returns

<table><thead><tr><th width="179">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The Price value adjusted for the decimal difference between base and quote currencies.</td></tr></tbody></table>

***

### toSignificant() - `public`

Rounds the Price to the significant digits specified.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>significantDigits</td><td>number</td><td>The number of significant digits to round to. Default is <code>6</code>.</td></tr><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications. Optional.</td></tr><tr><td>rounding</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L11">Rounding</a></td><td>Specifies the rounding logic used. Default is <a href="https://mikemcl.github.io/decimal.js-light/#modes"><code>ROUND_HALF_UP</code></a> which rounds to the nearest neighbour and rounds up if equidistant.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final price value rounded to the specified significant digits.</td></tr></tbody></table>

***

### toFixed() - `public`

Rounds the Price to the fixed number of decimals specified.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>decimalPlaces</td><td>number</td><td>The number of decimal places to round to. Default is <code>4</code>.</td></tr><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications. Optional.</td></tr><tr><td>rounding</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L11">Rounding</a></td><td>Specifies the rounding logic used. Default is <a href="https://mikemcl.github.io/decimal.js-light/#modes"><code>ROUND_HALF_UP</code></a> which rounds to the nearest neighbour and rounds up if equidistant.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final price value rounded to the decimal places specified.</td></tr></tbody></table>
