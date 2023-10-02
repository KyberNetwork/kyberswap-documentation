# SwapQuoter

{% hint style="info" %}
Handles the encoding of calldata required to call the quoter contract.



**GitHub File:** [quoter.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/quoter.ts)
{% endhint %}

* [Currency](https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4)

## Properties

### Public

<table><thead><tr><th width="136">Property</th><th width="129">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>INTERFACE</td><td><a href="https://www.npmjs.com/package/@ethersproject/abi">Interface</a></td><td>static</td><td>The Application Binary Interface for the related Elastic contracts.</td></tr></tbody></table>

## Methods

### quoteCallParameters() - `public` `static`

Based on the input parameters, handles the encoding of the relevant on-chain method that enables safe request for quotes.

#### Parameters

<table><thead><tr><th width="126">Params</th><th width="171">Type</th><th>Description</th></tr></thead><tbody><tr><td>route</td><td><a href="route.md">Route</a>&#x3C;TInput, TOutput></td><td>Array of potential pools with the same pair through which the swap can be routed. Ordered by the route the swap will take.</td></tr><tr><td>amount</td><td><a href="../../core-sdk/classes/currencyamount.md">CurrencyAmount</a>&#x3C;TInput, TOutput></td><td>The quote amount in either amount in or amount out. Direction is determined by the <code>tradeType</code>.</td></tr><tr><td>tradeType</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L6">TradeType</a></td><td>The type of trade: exact in OR exact out.</td></tr><tr><td>options</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/quoter.ts#L12">QuoteOptions</a></td><td>Default is <code>{}</code>.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/utils/calldata.ts#L6">MethodParameters</a></td><td>An object containing:<br><br><code>calldata: string</code> = The hex encoded calldata to perform the given operation.<br><br><code>value: string</code> = The amount of ether (wei) to send in hex.</td></tr></tbody></table>
