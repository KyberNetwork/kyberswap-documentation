# Ether

{% hint style="info" %}
Ether represents the ETH native currency on chains which do not implement their own native currencies (i.e. ARB, Linea, etc.).



**GitHub File:** [`ether.ts`](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/ether.ts)
{% endhint %}

## Extends

* [NativeCurrency](nativecurrency.md)

## Properties

#### Public

<table><thead><tr><th width="127">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>chainId</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/chain.ts#L1">ChainId</a></td><td>readonly</td><td>The chain ID on which this currency resides. See <a href="../../../getting-started/supported-exchanges-and-networks.md">supported chains</a>.</td></tr><tr><td>chainType</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/chain.ts#L29">ChainType</a></td><td>readonly</td><td>The virtual machine environment. Currently supports <a href="https://ethereum.org/en/developers/docs/evm/">EVM</a> only.</td></tr><tr><td>decimals</td><td>number</td><td>readonly</td><td>Number of decimals for the currency.</td></tr><tr><td>symbol</td><td>string</td><td>readonly</td><td>The currency symbol. Optional.</td></tr><tr><td>name</td><td>string</td><td>readonly</td><td>The currency name. Optional.</td></tr><tr><td>isNative</td><td>boolean</td><td>readonly</td><td>Whether the currency is native to the chain and must be wrapped.</td></tr><tr><td>isToken</td><td>boolean</td><td>readonly</td><td>Whether the currency meets the ERC20 standard and if not, needs to be wrapped.</td></tr></tbody></table>

### Private

<table><thead><tr><th width="145">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>_etherCache</td><td>Ether</td><td>static</td><td>Object to store Ether information across instances of this class.</td></tr></tbody></table>

## Constructor

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>chainId</td><td>number</td><td>The chain ID on which this currency resides. See <a href="../../../getting-started/supported-exchanges-and-networks.md">supported chains</a>.</td></tr></tbody></table>

## Methods

### wrapped() - `public` `get`

Accessor that returns the ERC20 wrapped version of Ether. Note that the token information for the nativeCurrency are stored in [`weth.ts`](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/weth.ts).

Note that the `invariant` function will throw if a _falsy_ value is detected. Refer to [tiny-invariant](https://www.npmjs.com/package/tiny-invariant) package for more details.

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>Token</td><td>The wrapped ERC20 token of Ether.</td></tr></tbody></table>

***

### onChain() - `public` `static`

Returns the Ethers instance for the chainId provided.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>chainId</td><td>number</td><td>The chain ID of the Ether instance being queried.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>Ether</td><td>The Ether instance on the chainId provided.</td></tr></tbody></table>

***

### equals() - `public`

Returns whether the currency passed in the argument is functionally equivalent to the Ether instance (i.e. the currency is tagged as a nativeCurrency and the chainIds are the same).

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4">Currency</a></td><td>The currency to check against.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td>Indicates whether the currency passed in the argument is functionally equivalent to the Ether instance.</td></tr></tbody></table>
