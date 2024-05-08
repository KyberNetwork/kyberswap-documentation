# Elastic Periphery Core Contracts

## Router[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#router) <a href="#router" id="router"></a>

The Router contract to handle swapping.

### Struct: ExactInputSingleParams[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#struct-exactinputsingleparams) <a href="#struct-exactinputsingleparams" id="struct-exactinputsingleparams"></a>

Contains data for swap exact input with a single pool.

```
ExactInputSingleParams
    address tokenIn;     // source token to swap
    address tokenOut;    // dest token to receive
    uint16 fee;          // fee of the pool to swap
    address recipient;   // the recipient of tokenOut
    uint256 deadline;    // deadline for the transaction
    uint256 amountIn;    // the amount of tokenIn to swap
    uint256 minAmountOut;// min acceptable amount of tokenOut
    uint160 limitSqrtP;  // the limit of sqrt price, partial swap if price reaches the limitation
```

### Struct: ExactInputParams[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#struct-exactinputparams) <a href="#struct-exactinputparams" id="struct-exactinputparams"></a>

Contains data for swap exact input with one or multiple pools.

```
ExactInputParams
    bytes path;           // contains data to identify list of pools to use for the swap
    address recipient;    // the recipient of token out
    uint256 deadline;     // deadline for the transaction
    uint256 amountIn;     // the amount of token in to swap
    uint256 minAmountOut; // the min acceptable amount of token out
```

### Struct: ExactOutputSingleParams[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#struct-exactoutputsingleparams) <a href="#struct-exactoutputsingleparams" id="struct-exactoutputsingleparams"></a>

Contains data for swap to an exact amount out of token out, using only one pool.

```
ExactOutputSingleParams:
    address tokenIn;    // source token to swap
    address tokenOut;   // dest token to receive
    uint16 fee;         // fee of the pool
    address recipient;  // the recipient of tokenOut
    uint256 deadline;   // deadline for the transaction
    uint256 amountOut;  // the amount of tokenOut to expect
    uint256 maxAmountIn;// the max amount of tokenIn that is allowed to use
    uint160 limitSqrtP; // the limit of sqrt price, partial swap if price reaches the limitation
```

### Struct: ExactOutputParams[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#struct-exactoutputparams) <a href="#struct-exactoutputparams" id="struct-exactoutputparams"></a>

Contains data for swap to an exact amount out of token out using one or multiple pools.

```
ExactOutputParams
    bytes path;
    address recipient;
    uint256 deadline;
    uint256 amountOut;
    uint256 maxAmountIn;
```

### `swapCallback()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#swapcallback) <a href="#swapcallback" id="swapcallback"></a>

```
Params:
    int256 deltaQty0
    int256 deltaQty1
    bytes data
```

Callback function that is be triggerred by the pool when swapping tokens. Either **deltaQty0** or **deltaQty1** must be positive. Positive value means the pool (also the caller) is expecting to receive that amount of token.

### `swapExactInputSingle()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#swapexactinputsingle) <a href="#swapexactinputsingle" id="swapexactinputsingle"></a>

```
Params:
    ExactInputSingleParams params
Returns:
    uint256 amountOut
```

Given the **params** of **ExactInputSingleParams**, it uses only one pool to swap exact an **amountIn** of **tokenIn** to **tokenOut** and return the amount of **tokenOut** from the swap. It calls the **swap** function in the pool contract, the pool will transfer the **tokenOut** to the **Router**, and expect to receive the corresponding **tokenIn** in the swap callback function.

### `swapExactInput()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#swapexactinput) <a href="#swapexactinput" id="swapexactinput"></a>

```
Params:
    ExactInputParams params
Returns:
    uint256 amountOut
```

Given the **params** of **ExactInputParams**, it uses only one or multiple pools that can be decoded from the **path**. It calls the **swap** function in each pool contract that is decoded from the **path** param, and uses callback to handle transferring tokens.

Flow:

* Swap path: _tokenIn -> token0 -> token1 -> ... -> tokenOut_.
* Call the first pool to borrow **token0** to the **Router**, then transfer **tokenIn** from user's wallet to the first pool.
* Call the second pool to borrow **token1** to the **Router**, then transfer **token0** from the **Router** to the second pool.
* Repeat the action until the last pool, and transfer **tokenOut** directly to the **recipient**.

### `swapExactOutputSingle()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#swapexactoutputsingle) <a href="#swapexactoutputsingle" id="swapexactoutputsingle"></a>

```
Params:
    ExactOutputSingleParams params
Returns:
    uint256 amountIn
```

Given the **params** of **ExactOutputSingleParams**, it uses only one pool to swap to get exact **amountOut** of **tokenOut** (or stop if price limit reaches).

* Call the **swap** function in the pool contract.
* The pool transfers the **tokenOut** to the **recipient**, and make the swap callback.
* The **Router** transfer the corresponding **tokenIn** from user's wallet to the pool. The required amount of **tokenIn** should not be greater than **maxAmountIn**.

### `swapExactOutput()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#swapexactoutput) <a href="#swapexactoutput" id="swapexactoutput"></a>

```
Params:
    ExactOutputParams params
Returns:
    uint256 amountIn
```

Given the **params** of **ExactOutputParams**, it uses one or multiple pools that can be decoded from the **path**. It calls the **swap** function in each pool contract that is decoded from the **path** param, and uses callback to handle transferring tokens. The list of pools in the **path** params should be in the reverse order, i.e the last pool first since we don't know the exact amount of token in to be used.

Flow:

* Origial swap path: _tokenIn -> token0 -> token1 -> ... -> tokenN -> tokenOut_.
* Reverse swap path: _tokenOut -> tokenN -> ... -> token1 -> token0 -> tokenIn_.
* Consider as we are swapping from **amountOut** of **tokenOut** to **tokenIn**.

## BasePositionManager[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#basepositionmanager) <a href="#basepositionmanager" id="basepositionmanager"></a>

Inherit from an ERC721 contract, it stores all positions of all liquidity providers and mint corresponding NFT.

Users can use the **PositionManager** to create & unlock pool, mint new position, add/remove liquidity to/from an existing position and burn their reinvestment tokens to receive back the LP fees.

It also inherits from **Multicall** contract, thus, users can make multiple function/method calls to the **PositionManager** in a single transaction.

All reinvestment tokens will be held in the contract, thus, it blocks anyone from transferring reinvestment tokens out. As a result, the contract can not support pools with any reinvestment tokens.

### Struct: MintParams[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#struct-mintparams) <a href="#struct-mintparams" id="struct-mintparams"></a>

Params for the first time adding liquidity, mint new nft to sender

```
MintParams
    address token0; // the token0 of the pool
    address token1; // token1 of the pool, must make sure that token0 < token1
    uint16 fee; // the pool's fee in bps
    int24 tickLower; // the position's lower tick
    int24 tickUpper; // the position's upper tick
    int24[2] ticksPrevious; // the nearest tick that has been initialized and lower than or equal to the tickLower and tickUpper, use to help insert the tickLower and tickUpper if haven't initialized
    uint256 amount0Desired; // the desired amount for token0
    uint256 amount1Desired; // the desired amount for token1
    uint256 amount0Min; // min amount of token 0 to add
    uint256 amount1Min; // min amount of token 1 to add
    address recipient; // the owner of the position
    uint256 deadline; // time that the transaction will be expired
```

### Struct: IncreaseLiquidityParams[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#struct-increaseliquidityparams) <a href="#struct-increaseliquidityparams" id="struct-increaseliquidityparams"></a>

Params for adding liquidity to the existing position

```
IncreaseLiquidityParams
    uint256 tokenId // id of the position to increase its liquidity
    uint256 amount0Desired // the desired amount for token0
    uint256 amount1Desired // the desired amount for token1
    uint256 amount0Min // min amount of token 0 to add
    uint256 amount1Min // min amount of token 1 to add
    uint256 deadline // time that the transaction will be expired
```

### Struct: RemoveLiquidityParams[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#struct-removeliquidityparams) <a href="#struct-removeliquidityparams" id="struct-removeliquidityparams"></a>

Params for remove liquidity from the existing position

```
RemoveLiquidityParams
    uint256 tokenId // id of the position to remove its liquidity
    uint256 amount0Min // min amount of token 0 to receive
    uint256 amount1Min // min amount of token 1 to receive
    uint256 deadline // time that the transaction will be expired
```

### Struct: BurnRTokenParams[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#struct-burnrtokenparams) <a href="#struct-burnrtokenparams" id="struct-burnrtokenparams"></a>

Burn the rTokens to get back token0 + token1 as fees

```
BurnRTokenParams
    uint256 tokenId // id of the position to burn r token
    uint256 amount0Min // min amount of token 0 to receive
    uint256 amount1Min // min amount of token 1 to receive
    uint256 deadline // time that the transaction will be expired
```

### `createAndUnlockPoolIfNecessary()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#createandunlockpoolifnecessary) <a href="#createandunlockpoolifnecessary" id="createandunlockpoolifnecessary"></a>

```
Params:
    address token0;
    address token1;
    uint16 fee;
    uint160 currentSqrtP
Returns:
    address pool // deployed pool given the set of params
```

Use this function to create & unlock a pool if needed given (**token0**, **token1**, **fee**) params and the initial sqrt price. Required: **token0 < token1**

### `mint()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#mint) <a href="#mint" id="mint"></a>

```
Params:
    MintParams params
Returns:
    uint256 tokenId;
    uint128 liquidity,
    uint256 amount0,
    uint256 amount1
```

Call the **\_addLiquidity** function in the **LiquidityHelper** contract with the data from \*_params_. It mints a new NFT token represents the position to the recipient, stores the position data and pool information.

### `addLiquidity()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#addliquidity) <a href="#addliquidity" id="addliquidity"></a>

```
Params:
    IncreaseLiquidityParams params
Returns:
    uint128 liquidity,
    uint256 amount0,
    uint256 amount1,
    uint256 additionalRTokenOwed
```

Call the **\_addLiquidity** function in the **LiquidityHelper** contract with the data from **params** to add more liquidity to a given position (i.e **tokenId**). Calculate and update the additional reinvestment tokens that the position should have earned.

### `removeLiquidity()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#removeliquidity) <a href="#removeliquidity" id="removeliquidity"></a>

```
Params:
    RemoveLiquidityParams params
Returns:
    uint256 amount0,
    uint256 amount1,
    uint256 additionalRTokenOwed
```

Call the **burn** function in the pool contract with the data from **params** to remove liquidity and get back 2 tokens. Calculate and update the additional reinvestment tokens that the position should have earned.

### `burnRTokens()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#burnrtokens) <a href="#burnrtokens" id="burnrtokens"></a>

```
Params:
    BurnRTokenParams params
Returns:
    uint256 rTokenQty,
    uint256 amount0,
    uint256 amount1
```

Call the **burnRTokens** function in the pool contract to burn all reinvestment tokens from the position and get back 2 tokens. Return the amount of reinvestment tokens to burn and expected amounts of 2 tokens to receive

#### Functions: `tokenURI()`, `getApproved()`, `_approve()`, `_getAndIncrementNonce()`[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#functions-tokenuri-getapproved-\_approve-\_getandincrementnonce) <a href="#functions-tokenuri-getapproved-_approve-_getandincrementnonce" id="functions-tokenuri-getapproved-_approve-_getandincrementnonce"></a>

Overriding functions for the inherited ERC721 and permit contracts.

## AntiSnipAttackPositionManager[​](https://docs.kyberswap.com/explanation/periphery-core-contracts#antisnipattackpositionmanager) <a href="#antisnipattackpositionmanager" id="antisnipattackpositionmanager"></a>

Inherits **BasePositionManager** and adds the anti-sniping attack feature into **addLiquidity** and **removeLiquidity** functions.

Reinvestment tokens of a position will be locked and vested to prevent LPs from adding then removing liquidity within a small period of time.

The motivation, mechanism and formula for Anti-Sniping Attack can be found [here](https://docs.google.com/document/d/1F50RWQRRyaNxnW5RvKgw09fN2FofIVLVccijgcOt-Iw/edit#heading=h.trv8zmis8u4c). The [AntiSnipingAttack library](https://docs.kyberswap.com/explanation/periphery-core-contracts#AntiSnipingAttack) will be of interest as well.
