# Tick

{% hint style="info" %}
Ticks partition the space of possible prices into discrete price ranges. Consequently, the infinite price range from 0 to ∞ is demarcated by evenly distributed discrete ticks. This tick design enables liquidity to be added within any two ticks. More details on the tick concept [here](https://docs.kyberswap.com/liquidity-solutions/kyberswap-elastic/concepts/tick-range-mechanism).



**GitHub File:** [tick.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/entities/tick.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="177">Property</th><th width="122">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>index</td><td>number</td><td>readonly</td><td>The index of the Tick which corresponds to a certain price.</td></tr><tr><td>liquidityGross</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>The gross tally of liquidity referencing the tick. Tick is uninitialized if liquidityGross is zero.</td></tr><tr><td>liquidityNet</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>readonly</td><td>Amount of liquidity added or subtracted to the pool's active liquidity when the tick is crossed.</td></tr></tbody></table>

## Constructor

### Parameters

<table><thead><tr><th width="177">Params</th><th width="122">Type</th><th>Description</th></tr></thead><tbody><tr><td>index</td><td>number</td><td>The index of the Tick which corresponds to a certain price.</td></tr><tr><td>liquidityGross</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The gross tally of liquidity referencing the tick. Tick is uninitialized if liquidityGross is zero.</td></tr><tr><td>liquidityNet</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>Amount of liquidity added or subtracted to the pool's active liquidity when the tick is crossed.</td></tr></tbody></table>
