# Route

{% hint style="info" %}
Describes a swap route which includes an ordered array of the tokens and pools with the same pair used in the swap.



**GitHub File:** [route.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/entities/route.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="177">Property</th><th width="122">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>pools</td><td><a href="pool.md">Pool</a>[]</td><td>readonly</td><td>Array of potential pools with the same pair through which the swap can be routed. Ordered by the route the swap will take.</td></tr><tr><td>tokenPath</td><td><a href="../../core-sdk/classes/token.md">Token</a>[]</td><td>readonly</td><td>Array of tokens through which the swap is routed. Ordered by the swap route whereby first token corresponds to the input token.</td></tr><tr><td>input</td><td>TInput</td><td>readonly</td><td>The input token for the swap.</td></tr><tr><td>output</td><td>TOutput</td><td>readonly</td><td>The output token for the swap.</td></tr></tbody></table>

### Private

<table><thead><tr><th width="175">Property</th><th width="230">Type</th><th>Description</th></tr></thead><tbody><tr><td>_midPrice</td><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;TInput, TOutput></td><td>The mid price of the route.</td></tr></tbody></table>

## Constructor

### Parameters

<table><thead><tr><th width="131">Params</th><th width="111">Type</th><th>Description</th></tr></thead><tbody><tr><td>pools</td><td><a href="pool.md">Pool</a>[]</td><td>Array of potential pools through which the swap can be routed. Ordered by the route the swap will take. The first pool must contain the input token and the last pool must contain the output token.</td></tr><tr><td>input</td><td>TInput</td><td>The input token for the swap.</td></tr><tr><td>output</td><td>TOutput</td><td>The output token for the swap.</td></tr></tbody></table>

## Methods

### chainId() - `public` `get`

Gets the chain ID for the chain on which the trade is taking place.

#### Returns

<table><thead><tr><th width="161">Type</th><th>Description</th></tr></thead><tbody><tr><td>number</td><td>The chainId for the route.</td></tr></tbody></table>

***

### midPrice() - `public` `get`

Returns the mid price of the route.

#### Returns

<table><thead><tr><th width="286">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../core-sdk/classes/price.md">Price</a>&#x3C;TInput, TOutput></td><td>The mid price of the route.</td></tr></tbody></table>
