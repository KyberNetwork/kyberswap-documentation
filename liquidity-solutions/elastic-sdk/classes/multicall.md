# Multicall

{% hint style="info" %}
Abstract class that enables the chaining of multiple calls into a single encoded message.



**GitHub File:** [multicall.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/multicall.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="136">Property</th><th width="129">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>INTERFACE</td><td><a href="https://www.npmjs.com/package/@ethersproject/abi">Interface</a></td><td>static</td><td>The Application Binary Interface for the related Elastic contracts.</td></tr></tbody></table>

## Constructor

Private constructor that cannot be constructed.

## Methods

### encodeMulticall() - `public` `static`

Returns a single encoded string representing all the calldata that was passed in. This enables multiple calls to be executed in a single transaction.

#### Parameters

<table><thead><tr><th width="117">Params</th><th width="112">Type</th><th>Description</th></tr></thead><tbody><tr><td>calldatas</td><td>calldatas: string | string[]</td><td>The calldata to be packaged into a single encoded string.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="162">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The encoded string that chains all the provided calldata.</td></tr></tbody></table>
