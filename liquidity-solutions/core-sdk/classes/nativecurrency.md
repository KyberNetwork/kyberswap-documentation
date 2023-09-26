# NativeCurrency

{% hint style="info" %}
NativeCurrency represents the currency of the chain on which it resides (i.e. the currency which is used to pay for gas on a particular chain). The NativeCurrency class ensures the equivalence of any native currency for the purposes of trades or queries.



**GitHub File:** [`nativeCurrency.ts`](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/nativeCurrency.ts)
{% endhint %}

## Extends

* [BaseCurrency](basecurrency.md)

## Properties

### Public

<table><thead><tr><th width="127">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>chainId</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/chain.ts#L1">ChainId</a></td><td>readonly</td><td>The chain ID on which this currency resides. See <a href="../../../getting-started/supported-exchanges-and-networks.md">supported chains</a>.</td></tr><tr><td>chainType</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/chain.ts#L29">ChainType</a></td><td>readonly</td><td>The virtual machine environment. Currently supports <a href="https://ethereum.org/en/developers/docs/evm/">EVM</a> only.</td></tr><tr><td>decimals</td><td>number</td><td>readonly</td><td>Number of decimals for the currency.</td></tr><tr><td>symbol</td><td>string</td><td>readonly</td><td>The currency symbol. Optional.</td></tr><tr><td>name</td><td>string</td><td>readonly</td><td>The currency name. Optional.</td></tr><tr><td>isNative</td><td>boolean</td><td>readonly</td><td>Whether the currency is native to the chain and must be wrapped.</td></tr><tr><td>isToken</td><td>boolean</td><td>readonly</td><td>Whether the currency meets the ERC20 standard and if not, needs to be wrapped.</td></tr></tbody></table>

## Constructor

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>chainId</td><td>number</td><td>The chain ID on which this currency resides. See <a href="../../../getting-started/supported-exchanges-and-networks.md">supported chains</a>.</td></tr><tr><td>decimals</td><td>number</td><td>Number of decimals for the currency.</td></tr><tr><td>symbol</td><td>string</td><td>The currency symbol. Optional.</td></tr><tr><td>name</td><td>string</td><td>The currency name. Optional.</td></tr></tbody></table>

## Methods

### wrapped() - `get`

Returns the ERC20 wrapped version of the native currency. Note that the token information for the nativeCurrency are stored in [`weth.ts`](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/weth.ts).

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>Token</td><td>The wrapped ERC20 token of the nativeCurrency.</td></tr></tbody></table>

***

### equals()

Returns whether the currency passed in the argument is functionally equivalent to the native currency (i.e. the currency is tagged as a nativeCurrency and the chainIds are the same).

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4">Currency</a></td><td>The currency to check against.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td>Indicates whether the currency passed in the argument is functionally equivalent to the native currency.</td></tr></tbody></table>
