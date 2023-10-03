# CurrencyAmount

{% hint style="info" %}
Enables the safe handling of currency amounts.\


**GitHub File:** [`currencyAmount.ts`](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/fractions/currencyAmount.ts)
{% endhint %}

## Extends

* [Currency](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/currency.ts)
* [Fraction](fraction.md)

## Properties

### Public

<table><thead><tr><th width="149">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>currency</td><td>T</td><td>readonly</td><td>The currency amount.</td></tr><tr><td>decimalScale</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>Number of decimals for the currency.</td></tr></tbody></table>

## Constructor - `protected`

#### Generics Type Definitions

<table><thead><tr><th width="222">Generics Name</th><th>Description</th></tr></thead><tbody><tr><td>T</td><td>Extends <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/currency.ts"><code>Currency</code></a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="149">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>currency</td><td>T</td><td>The currency.</td></tr><tr><td>numerator</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The numerator currency amount to be created.</td></tr><tr><td>denominator</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The denominator currency amount to be created. Optional.</td></tr></tbody></table>

## Methods

### fromRawAmount() - `public` `static`

Returns a new currency amount instance from the unitless amount of token (i.e. the raw amount).

#### Parameters

<table><thead><tr><th width="151">Params</th><th width="199">Type</th><th>Description</th></tr></thead><tbody><tr><td>currency</td><td>T</td><td>The currency.</td></tr><tr><td>rawAmount</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a> | <a href="https://www.npmjs.com/package/bn.js">BN</a></td><td>The unitless amount of tokens.</td></tr></tbody></table>

Returns

<table><thead><tr><th width="212">Type</th><th>Description</th></tr></thead><tbody><tr><td>CurrencyAmount&#x3C;T></td><td>The amount of currency in the specified currency amount format.</td></tr></tbody></table>

***

### fromFractionalAmount() - `public` `static`

Returns a new currency amount instance with a denominator that is not equal to 1.

#### Parameters

<table><thead><tr><th width="151">Params</th><th width="143">Type</th><th>Description</th></tr></thead><tbody><tr><td>currency</td><td>T</td><td>The currency.</td></tr><tr><td>numerator</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The numerator of the fractional token amount.</td></tr><tr><td>denominator</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a> </td><td>The denominator of the fractional token amount.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="212">Type</th><th>Description</th></tr></thead><tbody><tr><td>CurrencyAmount&#x3C;T></td><td>The amount of currency in the specified currency amount format.</td></tr></tbody></table>

***

### add() - `public`

Adds the provided currencyAmount to the CurrencyAmount instance and returns the result as a new currencyAmount.

#### Parameters

<table><thead><tr><th width="119">Params</th><th width="209">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>CurrencyAmount&#x3C;T></td><td>The currencyAmount to be added to the CurrencyAmount instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="212">Type</th><th>Description</th></tr></thead><tbody><tr><td>CurrencyAmount&#x3C;T></td><td>The currencyAmount representing the sum of the two currencyAmounts.</td></tr></tbody></table>

***

### subtract() - `public`

Subtracts/minuses the provided currencyAmount from the CurrencyAmount instance and returns the result as a new currencyAmount.

#### Parameters

<table><thead><tr><th width="119">Params</th><th width="209">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>CurrencyAmount&#x3C;T></td><td>The currencyAmount to be subtracted from the CurrencyAmount instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="212">Type</th><th>Description</th></tr></thead><tbody><tr><td>CurrencyAmount&#x3C;T></td><td>The final currencyAmount after subtracting the given currencyAmount from the CurrencyAmount instance.</td></tr></tbody></table>

***

### multiply() - `public`

Multiplies the CurrencyAmount instance with the provided currencyAmount and returns the result as a new currencyAmount.

#### Parameters

<table><thead><tr><th width="119">Params</th><th width="209">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>CurrencyAmount&#x3C;T></td><td>The currencyAmount to be multiplied with the CurrencyAmount instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="212">Type</th><th>Description</th></tr></thead><tbody><tr><td>CurrencyAmount&#x3C;T></td><td>The final currencyAmount after multiplying the given currencyAmount with the CurrencyAmount instance.</td></tr></tbody></table>

***

### divide() - `public`

Divides the currencyAmount instance with the provided currencyAmount and returns the result as a new currencyAmount.

#### Parameters

<table><thead><tr><th width="119">Params</th><th width="209">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>CurrencyAmount&#x3C;T></td><td>The currencyAmount to be divided from the CurrencyAmount instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="212">Type</th><th>Description</th></tr></thead><tbody><tr><td>CurrencyAmount&#x3C;T></td><td>The final currencyAmount after dividing the CurrencyAmount instance by the provided currencyAmount.</td></tr></tbody></table>

***

### toSignificant() - `public`

Rounds the CurrencyAmount instance to the significant digits specified.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>significantDigits</td><td>number</td><td>The number of significant digits to round to. Default is <code>6</code> digits.</td></tr><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications.</td></tr><tr><td>rounding</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L11">Rounding</a></td><td>Specifies the rounding logic used. Default is <a href="https://mikemcl.github.io/decimal.js-light/#modes"><code>ROUND_DOWN</code></a> which rounds towards zero.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final quotient value rounded to the specified significant digits.</td></tr></tbody></table>

***

### toFixed() - `public`

Rounds the currencyAmount instance to the fixed number of decimals specified.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>decimalPlaces</td><td>number</td><td>The number of decimal places to round to. Default is the currency's decimal places.</td></tr><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications.</td></tr><tr><td>rounding</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L11">Rounding</a></td><td>Specifies the rounding logic used. Default is <a href="https://mikemcl.github.io/decimal.js-light/#modes"><code>ROUND_DOWN</code></a> which rounds towards zero.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final quotient value rounded to the decimal places specified.</td></tr></tbody></table>

***

### toExact() - `public`&#x20;

Gets the exact CurrencyAmount instance value with the default currency decimals.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final exact quotient value down to the currency's default decimals.</td></tr></tbody></table>

***

### wrapped() - `public` `get`

Returns the wrapped version of the currencyAmount instance after accounting for whether the currency is a [Token](token.md) or [NativeCurrency](nativecurrency.md).

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>Token</td><td>The wrapped version of the currencyAmount instance.</td></tr></tbody></table>
