# NoTickDataProvider

{% hint style="info" %}
Throws an error whenever tick data is is required. Useful in cases where tick data is not required.



**GitHub File:** [tickDataProvider.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/entities/tickDataProvider.ts)
{% endhint %}

## Properties

### Private

<table><thead><tr><th width="189">Property</th><th width="122">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>ERROR_MESSAGE</td><td>string</td><td>static</td><td>Error message to throw whenever tick data is required but has not been provided.</td></tr></tbody></table>

## Methods

### getTick() - `async`

Throws a data provider error when tick data is queried.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>_tick</td><td>number</td><td>The tick index to query.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="241">Type</th><th>Description</th></tr></thead><tbody><tr><td>Promise&#x3C;{ liquidityNet: <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16">BigintIsh</a>}></td><td>Data provider error: 'No tick data provider was given'</td></tr></tbody></table>

***

### nextInitializedTickWithinOneWord() - `async`

Throws a data provider error when searching for the next initialized tick.

#### Parameters

<table><thead><tr><th width="147">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>_tick</td><td>number</td><td>The tick index to query.</td></tr><tr><td>_lte</td><td>boolean</td><td>Less than or equal to the starting tick. This determines whether to search for the next initialized tick to the left of the current tick.</td></tr><tr><td>_tickSpacing</td><td>number</td><td>The spacing between usable ticks.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="241">Type</th><th>Description</th></tr></thead><tbody><tr><td>Promise&#x3C;[number, boolean]></td><td>Data provider error: 'No tick data provider was given'</td></tr></tbody></table>

***

### nextInitializedTickWithinFixedDistance() - `async`

Throws a data provider error when searching for the next initialized tick.

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>_tick</td><td>number</td><td>The tick index to query.</td></tr><tr><td>_lte</td><td>boolean</td><td>Less than or equal to the starting tick. This determines whether to search for the next initialized tick to the left of the current tick.</td></tr><tr><td>_distance</td><td>number</td><td>The distance from the current active tick to search. Default is <code>480</code>.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="241">Type</th><th>Description</th></tr></thead><tbody><tr><td>Promise&#x3C;[number, boolean]></td><td>Data provider error: 'No tick data provider was given'</td></tr></tbody></table>
