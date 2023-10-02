# TickMath

{% hint style="info" %}
Contains the math to compute corresponding ticks and square root ratios (i.e. price).



**GitHub File:** [tickMath.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/utils/tickMath.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="187">Property</th><th width="112">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>MIN_TICK</td><td>number</td><td>static</td><td>The minimum tick of the pool.</td></tr><tr><td>MAX_TICK</td><td>number</td><td>static</td><td>The maximum tick of the pool.</td></tr><tr><td>MIN_SQRT_RATIO</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>static</td><td>The square root ratio (i.e. price) corresponding to the minimum tick.</td></tr><tr><td>MAX_SQRT_RATIO</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>static</td><td>The square root ratio (i.e. price) corresponding to the maximum tick.</td></tr></tbody></table>

## Constructor

Private constructor that cannot be constructed.

## Methods

### getSqrtRatioAtTick() - `public` `static`

Computes the square root ratio (i.e. price) at the specified tick.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>tick</td><td>number</td><td>The tick for which to compute the price.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The square root ratio at the specified tick.</td></tr></tbody></table>

***

### getTickAtSqrtRatio() - `public` `static`

Computes the tick corresponding to the specified square root ratio (i.e. price).

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>sqrtRatioX96</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The square root ratio (i.e. price) at which to calculate the corresponding tick.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The tick corresponding to the square root ratio.</td></tr></tbody></table>
