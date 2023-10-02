# SwapRouter

{% hint style="info" %}
Handles the encoding of calldata for swap routing.



**GitHub File:** [swapRouter.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/swapRouter.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="136">Property</th><th width="129">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>INTERFACE</td><td><a href="https://www.npmjs.com/package/@ethersproject/abi">Interface</a></td><td>static</td><td>The Application Binary Interface for the related Elastic contracts.</td></tr></tbody></table>

## Constructor

Private constructor that cannot be constructed.

## Methods

### swapCallParameters() - `public` `static`

Based on the input parameters, handles the encoding of the relevant on-chain method that enables safe execution of swap routes.

#### Parameters

<table><thead><tr><th width="125">Params</th><th width="217">Type</th><th>Description</th></tr></thead><tbody><tr><td>trades</td><td><a href="trade.md">Trade</a>&#x3C;<a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4">Currency</a>, <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4">Currency</a>, <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L6">TradeType</a>> | <a href="trade.md">Trade</a>&#x3C;<a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4">Currency</a>, <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4">Currency</a>, <a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L6">TradeType</a>>[]</td><td>The trade to produce call parameters for.</td></tr><tr><td>options</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/selfPermit.ts#L22">PermitOptions</a></td><td>The options for the swap operation:<br><br><code>slippageTolerance:</code><a href="../../core-sdk/classes/percent.md"><code>Percent</code></a> = The % amount that the executed price can differ from the expected price before the transaction will revert.<br><br><code>recipient: string</code> = The address to which the output tokens will be sent to.<br><br><code>deadline:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = Time after which the fee collection transaction will fail, in epoch seconds.<br><br><code>inputTokenPermit:</code><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/selfPermit.ts#L22"><code>PermitOptions</code></a> = The permit options for the input token. Optional.<br><br><code>sqrtPriceLimitX96:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = The price limit for the trade. Optional.<br><br><code>fee:</code><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/payments.ts#L7"><code>FeeOptions</code></a> = The fee options for the trade. Optional.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/utils/calldata.ts#L6">MethodParameters</a></td><td>An object containing:<br><br><code>calldata: string</code> = The hex encoded calldata to perform the given operation.<br><br><code>value: string</code> = The amount of ether (wei) to send in hex.</td></tr></tbody></table>
