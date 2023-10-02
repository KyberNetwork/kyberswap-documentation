# TickListDataProvider

{% hint style="info" %}
Provides information about ticks in a fixed list that is created upon class instantiation.



**GitHub File:** [tickListDataProvider.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/entities/tickListDataProvider.ts)
{% endhint %}

## Properties

### Private

<table><thead><tr><th width="177">Property</th><th width="122">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td><a href="tick.md">Tick</a>[]</td><td>readonly</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr></tbody></table>

## Constructor

### Parameters

<table><thead><tr><th width="139">Params</th><th width="216">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticks</td><td>(<a href="tick.md">Tick</a> | <a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/entities/tick.ts#L6">TickConstructorArgs</a>)[]</td><td>Array of ticks, each with information on the tick index and liquidity values associated with the tick.</td></tr><tr><td>tickSpacing</td><td>number</td><td>The tick spacing. Used to validate correct tick spacing and check pool liquidity against the total net liquidity across ticks.</td></tr></tbody></table>

## Methods

### getTick() - `async`

Returns the liquidity data of the tick index provided.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>tick</td><td>number</td><td>The tick index to query.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="241">Type</th><th>Description</th></tr></thead><tbody><tr><td>Promise&#x3C;{ liquidityNet: <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a>; liquidityGross: <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a> }></td><td>The <a href="tick.md#properties">liquidityNet</a> and <a href="tick.md#properties">liquidityGross</a> values for the tick index passed.</td></tr></tbody></table>

***

### nextInitializedTickWithinOneWord() - `async`

Searches the current and neighbouring words and returns the next initialized tick.&#x20;

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>tick</td><td>number</td><td>The tick index to query.</td></tr><tr><td>lte</td><td>boolean</td><td>Less than or equal to the starting tick. This determines whether to search for the next initialized tick to the left of the current tick.</td></tr><tr><td>tickSpacing</td><td>number</td><td>The spacing between usable ticks.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="241">Type</th><th>Description</th></tr></thead><tbody><tr><td>number</td><td>The next initialized tick up to 256 ticks away from the current active tick. If the next initialized tick is not within ±256 ticks, the value returned will be the last uninitialized tick from the current active tick (currentTick - 256 OR currentTick + 256).</td></tr><tr><td>boolean</td><td><code>true</code> = The tick number returned is initialized.<br><code>false</code> = The tick number returned is uninitialized.</td></tr></tbody></table>

***

### nextInitializedTickWithinFixedDistance() - `async`

Searches for the next initialized tick up to the distance specified.

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>tick</td><td>number</td><td>The tick index to query.</td></tr><tr><td>lte</td><td>boolean</td><td>Less than or equal to the starting tick. This determines whether to search for the next initialized tick to the left of the current tick.</td></tr><tr><td>distance</td><td>number</td><td>The distance from the current active tick to search. Default is <code>480</code>.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="241">Type</th><th>Description</th></tr></thead><tbody><tr><td>number</td><td>The next initialized tick up to the distance specified from current active tick. If the next initialized tick is not within the distance specified, the value returned will be the last uninitialized tick from the current active tick (currentTick - distance OR currentTick + distance).</td></tr><tr><td>boolean</td><td><code>true</code> = The tick number returned is initialized.<br><code>false</code> = The tick number returned is uninitialized.</td></tr></tbody></table>
