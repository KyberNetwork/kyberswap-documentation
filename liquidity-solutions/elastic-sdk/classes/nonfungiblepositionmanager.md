# NonfungiblePositionManager

{% hint style="info" %}
Handles the encoding of calldata for various position NFT operations.



**GitHub File:** [nonfungiblePositionManager.ts](https://github.com/KyberNetwork/ks-sdk-elastic/blob/main/src/nonfungiblePositionManager.ts)
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="136">Property</th><th width="129">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>INTERFACE</td><td><a href="https://www.npmjs.com/package/@ethersproject/abi">Interface</a></td><td>static</td><td>The Application Binary Interface for the related Elastic contracts.</td></tr></tbody></table>

## Constructor

Private constructor that cannot be constructed.

## Methods

### encodeCreate() - `private` `static`

Handles the encoding of calldata to create a new position if the pool does not exist. Additionally, unlocks/initializes a created pool to enable pool interactions.

#### Parameters

<table><thead><tr><th width="117">Params</th><th width="112">Type</th><th>Description</th></tr></thead><tbody><tr><td>pool</td><td><a href="pool.md">Pool</a></td><td>The pool to create and initialize.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="162">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The address of the pool that has been created/initialized. Formatted as a <a href="https://docs.ethers.org/v5/api/utils/abi/interface/#Interface--encoding">DataHexString</a>.</td></tr></tbody></table>

***

### createCallParameters() - `public` `static`

Add `0` hex value parameter to the [`encodeCreate()`](nonfungiblepositionmanager.md#encodecreate-private-static) function.

#### Parameters

<table><thead><tr><th width="142">Params</th><th width="112">Type</th><th>Description</th></tr></thead><tbody><tr><td>pool</td><td><a href="pool.md">Pool</a></td><td>The pool to create and initialize.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/utils/calldata.ts#L6">MethodParameters</a></td><td>An object containing:<br><br><code>calldata: string</code> = The hex encoded calldata to perform the given operation.<br><br><code>value: string</code> = The amount of ether (wei) to send in hex.</td></tr></tbody></table>

***

### createCallParametersTest() - `public` `static`

Add ETH hex value parameter to the [`encodeCreate()`](nonfungiblepositionmanager.md#encodecreate-private-static) function.

#### Parameters

<table><thead><tr><th width="142">Params</th><th width="112">Type</th><th>Description</th></tr></thead><tbody><tr><td>pool</td><td><a href="pool.md">Pool</a></td><td>The pool to create and initialize.</td></tr><tr><td>ethAmount</td><td><a href="https://www.npmjs.com/package/jsbi">JSBI</a></td><td>The ETH amount (in wei) to be added to the value paramter.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/utils/calldata.ts#L6">MethodParameters</a></td><td>An object containing:<br><br><code>calldata: string</code> = The hex encoded calldata to perform the given operation.<br><br><code>value: string</code> = The amount of ether (wei) to send in hex.</td></tr></tbody></table>

***

### addCallParameters() - `public` `static`

Handles the encoding of calldata to mint a new position or add liquidity to an existing position.

#### Parameters

<table><thead><tr><th width="142">Params</th><th width="200">Type</th><th>Description</th></tr></thead><tbody><tr><td>position</td><td><a href="position.md">Position</a> | <a href="position.md">Position</a>[]</td><td>The position(s) to create or add liquidity to.</td></tr><tr><td>ticks</td><td>number[] | number[][]</td><td>The previous ticks where liquidity was added to a position.</td></tr><tr><td>options</td><td>AddLiquidityOptions</td><td>The type of liquidity addition operation:<br><br><code>MintOptions</code> = Create a new position.<br><br><code>IncreaseOptions</code> = Add liquidity to existing position.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/utils/calldata.ts#L6">MethodParameters</a></td><td>An object containing:<br><br><code>calldata: string</code> = The hex encoded calldata to perform the add liquidity operations.<br><br><code>value: string</code> = The amount of ether (wei) to send in hex.</td></tr></tbody></table>

***

### encodeCollect() - `private` `static`

Handles the encoding of calldata to collect fees accrued to the position.

#### Parameters

<table><thead><tr><th width="106">Params</th><th width="147">Type</th><th>Description</th></tr></thead><tbody><tr><td>options</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/nonfungiblePositionManager.ts#L98">CollectOptions</a></td><td>An object consisting of fee collection data:<br><br><code>tokenId:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = The position ID from which to collect fees.<br><br><code>expectedCurrencyOwed0:</code><a href="../../core-sdk/classes/currencyamount.md"><code>CurrencyAmount</code></a><code>&#x3C;</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/currency.ts"><code>Currency</code></a><code>></code> = Estimated token0 fees owed to the position owner. Includes liquidity value to be burned.<br><br><code>expectedCurrencyOwed1:</code><a href="../../core-sdk/classes/currencyamount.md"><code>CurrencyAmount</code></a><code>&#x3C;</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/main/src/entities/currency.ts"><code>Currency</code></a><code>></code> = Estimated token1 fees owed to the position owner. Includes liquidity value to be burned.<br><br><code>recipient: string</code> = Account to receive the fee tokens.<br><br><code>deadline:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = Time after which the fee collection transaction will fail.<br><br><code>isRemovingLiquid: boolean</code> = <code>true</code> -> Liquidity is being removed together with the fee collection; <code>false</code> -> Only the fees are being collected. Optional.<br><br><code>havingFee: boolean</code> = <code>true</code> -> Position has accrued fees iwhich have been reinvested; <code>false</code> -> Position has yet to accrue any fees. Optional.<br><br><code>isPositionClosed: boolean</code> = <code>true</code> -> Position has been closed; <code>false</code> -> Position is still active. Optional.<br><br><code>legacyMode: boolean</code> = <code>true</code> -> Position supports <a href="https://docs.kyberswap.com/liquidity-solutions/kyberswap-elastic/concepts/pool-process-flows#implementation-details">syncFeeGrowth</a>; <code>false</code> -> Position does not support <a href="https://docs.kyberswap.com/liquidity-solutions/kyberswap-elastic/concepts/pool-process-flows#implementation-details">syncFeeGrowth</a>. Optional.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>string[]</td><td>The hex encoded calldata to perform the collect fee operations.</td></tr></tbody></table>

***

### collectCallParameters() - `public` `static`

Add `0` hex value parameter to the [`encodeCollect()`](nonfungiblepositionmanager.md#encodecollect-private-static) function.

#### Parameters

<table><thead><tr><th width="106">Params</th><th width="147">Type</th><th>Description</th></tr></thead><tbody><tr><td>options</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/nonfungiblePositionManager.ts#L98">CollectOptions</a></td><td>See <a href="nonfungiblepositionmanager.md#encodecollect-private-static">encodeCollect()</a> parameters.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/utils/calldata.ts#L6">MethodParameters</a></td><td>An object containing:<br><br><code>calldata: string</code> = The hex encoded calldata to perform the given operation.<br><br><code>value: string</code> = The amount of ether (wei) to send in hex.</td></tr></tbody></table>

***

### removeCallParameters() - `public` `static`

Handles the encoding of calldata to remove a position's liquidity.

#### Parameters

<table><thead><tr><th width="110">Params</th><th width="191">Type</th><th>Description</th></tr></thead><tbody><tr><td>options</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/nonfungiblePositionManager.ts#L72">SafeTransferOptions</a></td><td>An object consisting of NFT transfer data:<br><br><code>sender: string</code> = The account sending the NFT.<br><br><code>recipient: string</code> = The account receiving the NFT.<br><br><code>tokenId:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = The position ID of the NFT being sent.<br><br><code>data: string</code> = The optional parameter that passes data to the <a href="https://docs.openzeppelin.com/contracts/3.x/api/token/erc721#IERC721Receiver"><code>onERC721Received</code></a> call for the staker</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/utils/calldata.ts#L6">MethodParameters</a></td><td>An object containing:<br><br><code>calldata: string</code> = The hex encoded calldata to perform the given operation.<br><br><code>value: string</code> = The amount of ether (wei) to send in hex.</td></tr></tbody></table>

***

### safeTransferFromParameters() - `public` `static`

Handles the encoding of calldata to transfer the position NFT from one address to another.

#### Parameters

<table><thead><tr><th width="120">Params</th><th width="226">Type</th><th>Description</th></tr></thead><tbody><tr><td>position</td><td><a href="position.md">Position</a></td><td></td></tr><tr><td>options</td><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/nonfungiblePositionManager.ts#L146">RemoveLiquidityOptions</a></td><td>An object consisting of liquidity removal data:<br><br><code>tokenId:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = The position ID form which to remove liquidity.<br><br><code>liquidityPercentage:</code><a href="../../core-sdk/classes/percent.md"><code>Percent</code></a> = The % of the position's liquidity to remove.<br><br><code>slippageTolerance:</code><a href="../../core-sdk/classes/percent.md"><code>Percent</code></a> = The % amount that the pool price price is allowed to move before the transaction will revert.<br><br><code>deadline:</code><a href="https://github.com/KyberNetwork/ks-sdk-core/blob/c265d1b09784660bb9aca6f0d080aace334c0ac4/src/constants.ts#L4C16-L4C16"><code>BigintIsh</code></a> = Time after which the fee collection transaction will fail, in epoch seconds.<br><br><code>burnToken: boolean</code> = <code>true</code> -> Position NFT is burned as entire position's liquidity is removed; <code>false</code> -> Position NFT is not burned as liquidiyt is only partially removed. Optional.<br><br><code>permit:</code><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/nonfungiblePositionManager.ts#L136"><code>NFTPermitOptions</code></a> = The permit options for transacting with the NFT in the case that the address sending the removal transaction is not the NFT owner. Optional.<br><br><code>collectOptions: Omit&#x3C;</code><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/nonfungiblePositionManager.ts#L98"><code>CollectOption</code></a><code>, 'tokenId'></code> = The collection parameters to be passed onto the collect fees function.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/KyberNetwork/ks-sdk-elastic/blob/ef95bce57f9eeebf7de7814e38022126bdc1269e/src/utils/calldata.ts#L6">MethodParameters</a></td><td>An object containing:<br><br><code>calldata: string</code> = The hex encoded calldata to perform the given operation.<br><br><code>value: string</code> = The amount of ether (wei) to send in hex.</td></tr></tbody></table>
