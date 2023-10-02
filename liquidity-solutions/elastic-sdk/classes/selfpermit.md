# SelfPermit

{% hint style="info" %}
Handles the encoding of calldata required to call permit on any [EIP-2612](https://eips.ethereum.org/EIPS/eip-2612) compliant token.&#x20;



**GitHub File:** [selfPermit.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/selfPermit.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="136">Property</th><th width="129">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>INTERFACE</td><td><a href="https://www.npmjs.com/package/@ethersproject/abi">Interface</a></td><td>static</td><td>The Application Binary Interface for the related Elastic contracts.</td></tr></tbody></table>

## Constructor

Private constructor that cannot be constructed.

## Methods

### encodePermit() - `public` `static`

Handles the encoding of calldata that permits the contract to spend the specified token from the message sender.

#### Parameters

<table><thead><tr><th width="141">Params</th><th width="146">Type</th><th>Description</th></tr></thead><tbody><tr><td>token</td><td><a href="../../core-sdk/classes/token.md">Token</a></td><td>The token to permit.</td></tr><tr><td>options</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/selfPermit.ts#L22">PermitOptions</a></td><td>The options for the permit operation.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="162">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The encoded data that permits the contract to spend the input token.</td></tr></tbody></table>
