# BaseCurrency

{% hint style="info" %}
A currency is any fungible financial instrument on the blockchain. This includes all tokens which implement the [ERC20](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/) token standard as well as chain-native coins (i.e. currencies used to pay for gas) such as ETH, MATIC, etc.

The BaseCurrency is an abstract class that contains basic information about the currency that is being traded and ensures currency equivalence when executing functions (i.e. are the two currencies that are being added the same currency).



**GitHub File:** [`baseCurrency.ts`](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/baseCurrency.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="127">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>chainId</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/chain.ts#L1">ChainId</a></td><td>readonly</td><td>The chain ID on which this currency resides. See <a href="../../../getting-started/supported-exchanges-and-networks.md">supported chains</a>.</td></tr><tr><td>chainType</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/chain.ts#L29">ChainType</a></td><td>readonly</td><td>The virtual machine environment. Currently supports <a href="https://ethereum.org/en/developers/docs/evm/">EVM</a> only.</td></tr><tr><td>decimals</td><td>number</td><td>readonly</td><td>Number of decimals for the currency.</td></tr><tr><td>symbol</td><td>string</td><td>readonly</td><td>The currency symbol. Optional.</td></tr><tr><td>name</td><td>string</td><td>readonly</td><td>The currency name. Optional.</td></tr></tbody></table>

### Abstract properties

<table><thead><tr><th width="127">Property</th><th width="109">Type</th><th width="103">Visibility</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>isNative</td><td>boolean</td><td>public</td><td>readonly</td><td>Returns whether the currency is native to the chain and must be wrapped.</td></tr><tr><td>isToken</td><td>boolean</td><td>public</td><td>readonly</td><td>Returns whether the currency meets the ERC20 standard and if not, needs to be wrapped.</td></tr></tbody></table>

## Constructor

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>chainId</td><td>number</td><td>The chain ID on which this currency resides. See <a href="../../../getting-started/supported-exchanges-and-networks.md">supported chains</a>.</td></tr><tr><td>decimals</td><td>number</td><td>Number of decimals for the currency.</td></tr><tr><td>symbol</td><td>string</td><td>The currency symbol. Optional.</td></tr><tr><td>name</td><td>string</td><td>The currency name. Optional.</td></tr></tbody></table>

Note that the `invariant` function will throw if a _falsy_ value is detected. Refer to [tiny-invariant](https://www.npmjs.com/package/tiny-invariant) package for more details.

## Methods

### equals() - `public` `abstract`

Returns whether the currency passed in the argument is functionally equivalent to the base currency.

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/currency.ts#L4">Currency</a></td><td>The currency to check against.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td>Indicates whether the currency passed in the argument is functionally equivalent to the base currency.</td></tr></tbody></table>

***

### wrapped() - `public` `abstract`

Accessor that gets the ERC20 wrapped version of the currency. KyberSwap smart contracts only supports ERC20 tokens.

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>Token</td><td>The ERC20 wrapped version of the base currency.</td></tr></tbody></table>
