# Payments

{% hint style="info" %}
Handles the encoding of calldata for payment operations.



**GitHub File:** [payments.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/payments.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="136">Property</th><th width="129">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>INTERFACE</td><td><a href="https://www.npmjs.com/package/@ethersproject/abi">Interface</a></td><td>static</td><td>The Application Binary Interface for the related Elastic contracts.</td></tr></tbody></table>

## Constructor

Private constructor that cannot be constructed.

## Methods

### encodeFeeBips() - `private` `static`

Encodes the fees and returns the fee value as a hexed string.

#### Parameters

<table><thead><tr><th width="117">Params</th><th width="112">Type</th><th>Description</th></tr></thead><tbody><tr><td>fee</td><td><a href="../../core-sdk/classes/percent.md">Percent</a></td><td>The fees charged for the payment</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="162">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>An encoded string that represents the hex value of the fee.</td></tr></tbody></table>

***

### encodeUnwrapETH() - `public` `static`

Handles the encoding of unwrapping WETH with the option to charge fees for the unwrapping operation.

#### Parameters

<table><thead><tr><th width="174">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>amountMinimum</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The minimum balance of the contract from which WETH is being unwrapped. Prevents malicious contracts from stealing WETH9 from users.</td></tr><tr><td>recipient</td><td>string</td><td>The recipient of the unwrapped ETH.</td></tr><tr><td>feeOptions</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/payments.ts#L7">FeeOptions</a></td><td>An object that contains fee data for the unwrap transaction:<br><br><code>fee:</code><a href="../../core-sdk/classes/percent.md"><code>Percent</code></a> = The % of the transfer output that will be taken as a fee.<br><br><code>recipient: string</code> = The recipient address for the fee.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="162">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The hex encoded calldata to perform the WETH unwrapping.</td></tr></tbody></table>

***

### encodeSweepToken() - `public` `static`

Handles the encoding of transferring all of a contract's `token` balance with an optional fee.

#### Parameters

<table><thead><tr><th width="174">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>token</td><td><a href="../../core-sdk/classes/token.md">Token</a></td><td>The token to be transferred/swept.</td></tr><tr><td>amountMinimum</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The minimum balance of the contract. Prevents malicious contracts from stealing WETH9 from users.</td></tr><tr><td>recipient</td><td>string</td><td>The recipient of the unwrapped ETH.</td></tr><tr><td>feeOptions</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/payments.ts#L7">FeeOptions</a></td><td>An object that contains fee data for the unwrap transaction:<br><br><code>fee:</code><a href="../../core-sdk/classes/percent.md"><code>Percent</code></a> = The % of the transfer output that will be taken as a fee.<br><br><code>recipient: string</code> = The recipient address for the fee.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="162">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The hex encoded calldata to perform the token sweep operation.</td></tr></tbody></table>

***

### encodeRefundETH() - `public` `static`

Handles the encoding of transferring all of a contract's ETH balance to the message sender.

#### Returns

<table><thead><tr><th width="162">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The hex encoded calldata to perform the ETH refund operation.</td></tr></tbody></table>
