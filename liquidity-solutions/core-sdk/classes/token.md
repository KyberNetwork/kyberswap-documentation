# Token

{% hint style="info" %}
Token represents an ERC20 token with a unique address and additional data on whether the token is a native currency. The Token class ensures Token equivalence when executing functions.



**GitHub File:** [`token.ts`](https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/token.ts)
{% endhint %}

## Extends

* [BaseCurrency](basecurrency.md)

## Properties

### Public

<table><thead><tr><th width="127">Property</th><th width="115">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>string</td><td>readonly</td><td>The token contract address.</td></tr><tr><td>chainId</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/chain.ts#L1">ChainId</a></td><td>readonly</td><td>The chain ID on which this currency resides. See <a href="../../../getting-started/supported-exchanges-and-networks.md">supported chains</a>.</td></tr><tr><td>chainType</td><td><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/entities/chain.ts#L29">ChainType</a></td><td>readonly</td><td>The virtual machine environment. Currently supports <a href="https://ethereum.org/en/developers/docs/evm/">EVM</a> only.</td></tr><tr><td>decimals</td><td>number</td><td>readonly</td><td>Number of decimals for the currency.</td></tr><tr><td>symbol</td><td>string</td><td>readonly</td><td>The currency symbol. Optional.</td></tr><tr><td>name</td><td>string</td><td>readonly</td><td>The currency name. Optional.</td></tr><tr><td>isNative</td><td>boolean</td><td>readonly</td><td>Whether the currency is native to the chain and must be wrapped.</td></tr><tr><td>isToken</td><td>boolean</td><td>readonly</td><td>Whether the currency meets the ERC20 standard and if not, needs to be wrapped.</td></tr></tbody></table>

Note that the `mint` property was previously used to manage Solana tokens but support for Solana on KyberSwap has since been deprecated.

## Constructor

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>chainId</td><td>number</td><td>The chain ID on which this currency resides. See <a href="../../../getting-started/supported-exchanges-and-networks.md">supported chains</a>.</td></tr><tr><td>address</td><td>string</td><td>The token contract address.</td></tr><tr><td>decimals</td><td>number</td><td>Number of decimals for the currency.</td></tr><tr><td>symbol</td><td>string</td><td>The currency symbol. Optional.</td></tr><tr><td>name</td><td>string</td><td>The currency name. Optional.</td></tr></tbody></table>

## Methods

### equals() - `public`

Returns whether the token passed in the argument is functionally equivalent to the token implementing this class (i.e. same contract address on the same chain).

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Token</td><td>The token to check against.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td>Indicates whether the token passed in the argument is functionally equivalent to the token implementing this class.</td></tr></tbody></table>

***

### sortsBefore() - `public`

Returns true if the token's contract address sorts before the input token contract address. Also checks if the tokens are equivalent else throws an error (i.e. same contract address and chain).

#### Parameters

<table><thead><tr><th width="127">Params</th><th width="115">Type</th><th>Description</th></tr></thead><tbody><tr><td>other</td><td>Token</td><td>The currency to check against.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>boolean</td><td><code>true</code> = Token's contract address sorts before input token address.<br><code>false</code> = Token's contract address sorts after input token address.</td></tr></tbody></table>

***

### wrapped() - `public` `get`

Accessor that returns this ERC20 token.

#### Returns

<table><thead><tr><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>Token</td><td>The token implementing this class.</td></tr></tbody></table>
