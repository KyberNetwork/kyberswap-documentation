# LiquidityMath

{% hint style="info" %}
Handles liquidity math.



**GitHub File:** [liquidityMath.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/utils/liquidityMath.ts)
{% endhint %}

## Constructor

Private constructor that cannot be constructed.

## Methods

### addDelta() - `public` `static`

Add a signed liquidity delta to liquidity.

#### Parameters

<table><thead><tr><th width="167">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>x</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Existing liquidity.</td></tr><tr><td>y</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Liquidity delta which to modify existing liquidity.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The liquidity delta.</td></tr></tbody></table>
