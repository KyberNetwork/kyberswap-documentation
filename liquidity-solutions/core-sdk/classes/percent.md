# Percent

{% hint style="info" %}
Enables the safe handling of percentages.



**GitHub File:** [percent.ts](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/fractions/percent.ts)
{% endhint %}

## Extends

* [Fraction](fraction.md)

## Properties

### Public

<table><thead><tr><th width="149">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>isPercent</td><td>true</td><td>readonly</td><td>Boolean if the Percent instance is a percentage value. Prevents fractions from being interpreted as a Percent.</td></tr></tbody></table>

## Constructor

Percent instances are derived from the [Fraction](fraction.md) class via the `toPercent()` function which takes a Fraction and converts it into a Percent. For each of the algorithmic methods in the Percent class, the `toPercent()` function is called after the Fraction calculations are completed.

## Methods

### add()

Adds the provided fraction to the Percent instance and returns the result as a new Percent.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="178">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to be added to the underlying Fraction value of the Percent instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="177">Type</th><th>Description</th></tr></thead><tbody><tr><td>Percent</td><td>The Percent value representing the sum of the two fractions.</td></tr></tbody></table>

***

### subtract()

Subtracts/minuses the provided fraction to the Percent instance and returns the result as a new Percent.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="178">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to be subtracted from the underlying Fraction value of the Percent instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="177">Type</th><th>Description</th></tr></thead><tbody><tr><td>Percent</td><td>The Percent after subtracting the given fraction from the underlying Fraction.</td></tr></tbody></table>

***

### multiply()

Multiplies the Percent instance with the provided fraction and returns the result as a new Percent.

#### Parameters

<table><thead><tr><th width="112">Params</th><th width="175">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to be multiplied with the underlying Fraction value of the Percent instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="116">Type</th><th>Description</th></tr></thead><tbody><tr><td>Percent</td><td>The Percent value after multiplying the given fraction with the underlying Fraction.</td></tr></tbody></table>

***

### divide()

Divides the Percent instance with the provided fraction and returns the result as a new Percent.

#### Parameters

<table><thead><tr><th width="112">Params</th><th width="175">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to be divided from the underlying Fraction value of the Percent instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The Percent value after dividing the underlying Fraction by the provided fraction.</td></tr></tbody></table>

***

### toSignificant()

Rounds the Percent to the significant digits specified.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>significantDigits</td><td>number</td><td>The number of significant digits to round to. Default is <code>5</code>.</td></tr><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications. Optional.</td></tr><tr><td>rounding</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L11">Rounding</a></td><td>Specifies the rounding logic used. Default is <a href="https://mikemcl.github.io/decimal.js-light/#modes"><code>ROUND_HALF_UP</code></a> which rounds to the nearest neighbour and rounds up if equidistant.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final Percent value rounded to the specified significant digits.</td></tr></tbody></table>

***

### toFixed()

Rounds the Percent to the fixed number of decimals specified.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>decimalPlaces</td><td>number</td><td>The number of decimal places to round to. Default is <code>2</code>.</td></tr><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications.</td></tr><tr><td>rounding</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L11">Rounding</a></td><td>Specifies the rounding logic used. Default is <a href="https://mikemcl.github.io/decimal.js-light/#modes"><code>ROUND_HALF_UP</code></a> which rounds to the nearest neighbour and rounds up if equidistant.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final Percent value rounded to the decimal places specified.</td></tr></tbody></table>
