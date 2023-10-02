# FullMath

{% hint style="info" %}
Handles core maths for multiplication, division, and quadratic root.



**GitHub File:** [fullMath.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/utils/fullMath.ts)
{% endhint %}

## Constructor

Private constructor that cannot be constructed.

## Methods

### mulDivRoundingUp() - `public` `static`

Divides the product of the params by the given denominator and rounds up to the nearest integer.&#x20;

$$result=\lceil{\frac{a{\cdot}b}{denominator}}\rceil$$

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>a</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The multiplicand.</td></tr><tr><td>b</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The multiplier.</td></tr><tr><td>denominator</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Denominator to divide the product of the multiplicand and multiplier.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Product of <code>a</code> and <code>b</code> divided by the <code>denominator</code>. Rounded up to the nearest integer.</td></tr></tbody></table>

***

### mulDiv() - `public` `static`

Divides the product of the params by the given denominator.&#x20;

$$result=\frac{a{\cdot}b}{denominator}$$

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>a</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>First parameter to multiply.</td></tr><tr><td>b</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Second parameter to multiply.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Product of <code>a</code> and <code>b</code> divided by the <code>denominator</code>.</td></tr></tbody></table>

***

### getSmallerRootOfQuadEqn() - `public` `static`

Returns the smaller root of a quadratic equation.

$$result = \frac{b-{\sqrt{{b^2}-ac}}}{a}$$

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>a</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>First quadratic coefficient.</td></tr><tr><td>b</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Second quadratic coefficient.</td></tr><tr><td>c</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Third quadratic coefficient.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Smallest root of the quadratic equation.</td></tr></tbody></table>
