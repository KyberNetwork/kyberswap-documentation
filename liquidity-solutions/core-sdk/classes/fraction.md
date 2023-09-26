# Fraction

{% hint style="info" %}
Enables the safe handling of fractional amounts.



**GitHub File:** [`fraction.ts`](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/fractions/fraction.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="149">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>numerator</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>The fraction's numerator.</td></tr><tr><td>denominator</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>The fraction's denominator.</td></tr></tbody></table>

## Constructor

#### Parameters

<table><thead><tr><th width="149">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>numerator</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The numerator of the fraction to be created.</td></tr><tr><td>denominator</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The denominator of the fraction to be created.</td></tr></tbody></table>

## Methods

### numberatorBN() - `public` `get`

Returns the Big Number equivalent of the numerator.

_Note the typo in the method name as the extra `b` has not been removed to avoid any disruptions._

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/bn.js">BN</a></td><td>The fraction's numerator returned as a Big Number type.</td></tr></tbody></table>

***

### denominatorBN() - `public` `get`

Returns the Big Number equivalent of the denominator.

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/bn.js">BN</a></td><td>The fraction's denominator returned as a Big Number type.</td></tr></tbody></table>

***

### tryParseFunction() - `private` `static`

Validates that the parameter passed is a fraction and returns the fraction.

#### Parameters

<table><thead><tr><th width="133">Params</th><th width="199">Type</th><th>Description</th></tr></thead><tbody><tr><td>fractionish</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a> | Fraction</td><td>The fraction to be parsed/validated.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The parsed Fraction</td></tr></tbody></table>

***

### quotient() - `public` `get`

Gets the result of dividing the fraction rounded down to the nearest integer.

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The quotient when the numerator is divided by the denominator.</td></tr></tbody></table>

***

### quotientBN() - `public` `get`

Gets the result of dividing the fraction rounded down to the nearest integer as a Big Number type.

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/bn.js">BN</a></td><td>The quotient when the numerator is divided by the denominator.</td></tr></tbody></table>

***

### remainder() - `public` `get`

Gets the remainder of dividing the fraction rounded down to the nearest integer.

#### Returns

<table><thead><tr><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The remainder Fraction when the numerator is divided by the denominator.</td></tr></tbody></table>

***

### invert() - `public`

Returns the inverted fraction of the Fraction instance.

#### Returns

<table><thead><tr><th width="177">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The fraction instance inverted.</td></tr></tbody></table>

***

### add() - `public`

Adds the provided fraction to the Fraction instance and returns the result as a new Fraction.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="178">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to be added to the Fraction instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="177">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The fraction representing the sum of the two fractions.</td></tr></tbody></table>

***

### subtract() - `public`

Subtracts/minuses the provided fraction to the Fraction instance and returns the result as a new Fraction.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="178">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to be subtracted from the Fraction instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="177">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The final fraction after subtracting the given fraction from the Fraction instance.</td></tr></tbody></table>

***

### lessThan() - `public`

Checks if the Fraction instance is less than the provided fraction.

#### Parameters

<table><thead><tr><th width="120">Params</th><th width="178">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to compare against the Fraction instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="177">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td><code>true</code> = Fraction instance is less than provided fraction.<br><code>false</code> = Fraction instance is greater than provided fraction.</td></tr></tbody></table>

***

### equalTo() - `public`

Checks if the Fraction instance is equal to the provided fraction.

#### Parameters

<table><thead><tr><th width="120">Params</th><th width="178">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to compare against the Fraction instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="177">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td><code>true</code> = Fraction instance is equal to the provided fraction.<br><code>false</code> = Fraction instance is not equal to the provided fraction.</td></tr></tbody></table>

***

### greaterThan() - `public`

Checks if the Fraction instance is greater than the provided fraction.

#### Parameters

<table><thead><tr><th width="120">Params</th><th width="178">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to compare against the Fraction instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="177">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td><code>true</code> = Fraction instance is greater than provided fraction.<br><code>false</code> = Fraction instance is less than provided fraction.</td></tr></tbody></table>

***

### multiply() - `public`

Multiplies the Fraction instance with the provided fraction and returns the result as a new Fraction.

#### Parameters

<table><thead><tr><th width="112">Params</th><th width="175">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to be multiplied with the Fraction instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="116">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The final fraction after multiplying the given fraction with the Fraction instance.</td></tr></tbody></table>

***

### divide() - `public`

Divides the Fraction instance with the provided fraction and returns the result as a new Fraction.

#### Parameters

<table><thead><tr><th width="112">Params</th><th width="175">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Fraction | <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a></td><td>The fraction to be divided from the Fraction instance.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>The final fraction after dividing the Fraction instance by the provided fraction.</td></tr></tbody></table>

***

### toSignificant() - `public`

Rounds the Fraction to the significant digits specified.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>significantDigits</td><td>number</td><td>The number of significant digits to round to.</td></tr><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications.</td></tr><tr><td>rounding</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L11">Rounding</a></td><td>Specifies the rounding logic used. Default is <a href="https://mikemcl.github.io/decimal.js-light/#modes"><code>ROUND_HALF_UP</code></a> which rounds to the nearest neighbour and rounds up if equidistant.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final quotient value rounded to the specified significant digits.</td></tr></tbody></table>

***

### toFixed() - `public`

Rounds the Fraction to the fixed number of decimals specified.

#### Parameters

<table><thead><tr><th width="192">Params</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>decimalPlaces</td><td>number</td><td>The number of decimal places to round to.</td></tr><tr><td>format</td><td>object</td><td>Configure output format per <a href="https://www.npmjs.com/package/toformat">toformat</a> specifications.</td></tr><tr><td>rounding</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L11">Rounding</a></td><td>Specifies the rounding logic used. Default is <a href="https://mikemcl.github.io/decimal.js-light/#modes"><code>ROUND_HALF_UP</code></a> which rounds to the nearest neighbour and rounds up if equidistant.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The final quotient value rounded to the decimal places specified.</td></tr></tbody></table>

***

### asFraction() - `public` `get`

Helper method for converting any super class back to a fraction.

#### Returns

<table><thead><tr><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>Fraction</td><td>Fraction representation of the super class.</td></tr></tbody></table>
