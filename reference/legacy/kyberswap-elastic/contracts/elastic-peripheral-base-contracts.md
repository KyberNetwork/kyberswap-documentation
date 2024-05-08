# Elastic Peripheral Base Contracts

## DeadlineValidation[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#deadlinevalidation) <a href="#deadlinevalidation" id="deadlinevalidation"></a>

Validate if the block timestamp has not reached the deadline yet, use for transactions with a deadline.

### Modifier: `onlyNotExpired()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#modifier-onlynotexpired) <a href="#modifier-onlynotexpired" id="modifier-onlynotexpired"></a>

Reverts if the current block's timestamp is greater than the specified `deadline`.

| Field      | Type      | Explanation                                          |
| ---------- | --------- | ---------------------------------------------------- |
| `deadline` | `uint256` | Timestamp to check against current block's timestamp |

### `_blockTimestamp()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#\_blocktimestamp) <a href="#_blocktimestamp" id="_blocktimestamp"></a>

Returns the current block timestamp. Used for overriding by mock contracts for tests.

## ERC721Permit[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#erc721permit) <a href="#erc721permit" id="erc721permit"></a>

Nonfungible tokens that support an approve via signature, i.e. permit for ERC721.

## ImmutableRouterStorage[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#immutablerouterstorage) <a href="#immutablerouterstorage" id="immutablerouterstorage"></a>

Immutable variables that are used by Periphery contracts.

### Immutables[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#immutables) <a href="#immutables" id="immutables"></a>

| Field          | Type      | Explanation                                                                                                           |
| -------------- | --------- | --------------------------------------------------------------------------------------------------------------------- |
| `factory`      | `address` | Factory contract address                                                                                              |
| `WETH`         | `address` | Canonical WETH address                                                                                                |
| `poolInitHash` | `bytes32` | keccak256 hash of the pool's creation code. Used to compute the pool address without reading storage from the Factory |

## RouterTokenHelper[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#routertokenhelper) <a href="#routertokenhelper" id="routertokenhelper"></a>

A helper contract to handle transfers, wrapping and unwrapping of tokens.

### `unwrapWeth()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#unwrapweth) <a href="#unwrapweth" id="unwrapweth"></a>

Unwraps the contract's entire **WETH** balance to **ETH**, then transfers them to the recipient.

| Input Field | Type      | Explanation                                                  |
| ----------- | --------- | ------------------------------------------------------------ |
| `minAmount` | `uint256` | Contract's WETH balance should not be lower than this amount |
| `recioient` | `address` | Desired recipient of unwrapped ETH                           |

### `transferAllTokens()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#transferalltokens) <a href="#transferalltokens" id="transferalltokens"></a>

Transfers the contract's entire `token` balance to the recipient

| Input Field | Type      | Explanation                                                   |
| ----------- | --------- | ------------------------------------------------------------- |
| `token`     | `address` | Token to transfer                                             |
| `minAmount` | `uint256` | Contract's token balance should not be lower than this amount |
| `recipient` | `address` | Desired recipient of the token                                |

### `refundEth()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#refundeth) <a href="#refundeth" id="refundeth"></a>

Transfers all **ETH** balance to the sender.

### `_transferTokens()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#\_transfertokens) <a href="#_transfertokens" id="_transfertokens"></a>

Internal function to help transfer tokens from the `sender` to the `recipient`. If `token` is **WETH** and the contract has enough **ETH** balance, then wrap and transfer **WETH**, otherwise use [RouterTokenHelper](elastic-peripheral-base-contracts.md#routertokenhelper) to handle transfers.

| Input Field | Type      | Explanation                        |
| ----------- | --------- | ---------------------------------- |
| `token`     | `address` | Token to transfer                  |
| `sender`    | `address` | Address to pull `token` funds from |
| `recipient` | `address` | Desired recipient of the token     |
| `amount`    | `uint256` | Amount to be transferred           |

## RouterTokenHelperWithFee[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#routertokenhelperwithfee) <a href="#routertokenhelperwithfee" id="routertokenhelperwithfee"></a>

Inherits [RouteTokenHelper](elastic-peripheral-base-contracts.md#routertokenhelper). Contains additional functions to charge a fee for transfers as well.

### `unwrapWethWithFee()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#unwrapwethwithfee) <a href="#unwrapwethwithfee" id="unwrapwethwithfee"></a>

Unwraps the contract's entire **WETH** balance to **ETH**, then transfers them to the `recipient`. Charges a fee which is transferred to `feeRecipient`

| Input Field    | Type      | Explanation                                                  |
| -------------- | --------- | ------------------------------------------------------------ |
| `minAmount`    | `uint256` | Contract's WETH balance should not be lower than this amount |
| `recipient`    | `address` | Desired recipient of unwrapped ETH                           |
| `feeBps`       | `uint256` | Fee to charge in basis points                                |
| `feeRecipient` | `address` | Address to receive the fee charged                           |

### `transferAllTokensWithFee()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#transferalltokenswithfee) <a href="#transferalltokenswithfee" id="transferalltokenswithfee"></a>

Transfers the contract's entire `token` balance to the recipient. Charges a fee which is transferred to `feeRecipient`.

| Input Field    | Type      | Explanation                                                   |
| -------------- | --------- | ------------------------------------------------------------- |
| `token`        | `address` | Token to transfer                                             |
| `minAmount`    | `uint256` | Contract's token balance should not be lower than this amount |
| `recipient`    | `address` | Desired recipient of the token                                |
| `feeBps`       | `uint256` | Fee to charge in basis points                                 |
| `feeRecipient` | `address` | Address to receive the fee charged                            |

## Multicall[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#multicall) <a href="#multicall" id="multicall"></a>

Enables calling multiple methods in a single call to the contract.

### `multicall()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#multicall-1) <a href="#multicall-1" id="multicall-1"></a>

Uses **`delegateCall`** to sequentially execute functions, then return the result of each execution.

**Input**[**​**](https://docs.kyberswap.com/explanation/peripheral-base-contracts#input)

| Field  | Type      | Explanation                                                          |
| ------ | --------- | -------------------------------------------------------------------- |
| `data` | `bytes[]` | encoded function data for each of the calls to make to this contract |

**Output**[**​**](https://docs.kyberswap.com/explanation/peripheral-base-contracts#output)

| Field     | Type      | Explanation                              |
| --------- | --------- | ---------------------------------------- |
| `results` | `bytes[]` | results from each of the calls passed in |

## LiquidityHelper[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#liquidityhelper) <a href="#liquidityhelper" id="liquidityhelper"></a>

A helper contract to handle liquidity related actions, including mint/add/remove liquidity.

### Struct: AddLiquidityParams[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#struct-addliquidityparams) <a href="#struct-addliquidityparams" id="struct-addliquidityparams"></a>

Used when minting a new position or adding liquidity to an existing one.

| Field            | Type       | Explanation                                                                                                                                                                |
| ---------------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `token0`         | `address`  | first token of the pool                                                                                                                                                    |
| `token1`         | `address`  | second token of the pool                                                                                                                                                   |
| `fee`            | `uint16`   | the pool's swap fee                                                                                                                                                        |
| `tickLower`      | `int24`    | position's lower tick                                                                                                                                                      |
| `tickUpper`      | `int24`    | position's upper tick                                                                                                                                                      |
| `ticksPrevious`  | `int24[2]` | an array containing 2 values `tickLowerPrevious` and `tickUpperPrevious` which are expected to be the nearest initialized tick <= `tickLower` and `tickUpper` respectively |
| `amount0Desired` | `uint256`  | token0 amount user wants to add                                                                                                                                            |
| `amount1Desired` | `uint256`  | token1 amount user wants to add                                                                                                                                            |
| `amount0Min`     | `uint256`  | minimum token0 amount that should be used                                                                                                                                  |
| `amount1Min`     | `uint256`  | minimum token1 amount that should be used                                                                                                                                  |

### Struct: CallbackData[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#struct-callbackdata) <a href="#struct-callbackdata" id="struct-callbackdata"></a>

Data for callback from Pool contract.

| Field    | Type      | Explanation                            |
| -------- | --------- | -------------------------------------- |
| `token0` | `address` | first token of the pool                |
| `token1` | `address` | second token of the pool               |
| `fee`    | `uint16`  | the pool's swap fee                    |
| `source` | `address` | address to transfer token0/token1 from |

### `proAMMMintCallback()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#proammmintcallback) <a href="#proammmintcallback" id="proammmintcallback"></a>

Mint callback function implementation called by a Pool.

| Input Field | Type      | Explanation                         |
| ----------- | --------- | ----------------------------------- |
| `deltaQty0` | `uint256` | token0 amount requested by the pool |
| `deltaQty1` | `uint256` | token1 amount requested by the pool |
| `data`      | `bytes`   | Encoded `CallbackData`              |

### `_addLiquidity()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#\_addliquidity) <a href="#_addliquidity" id="_addliquidity"></a>

Add liquidity to a pool. _token0_ and _token1_ should be in the correct order, i.e _token0 < token1_.

**Input**[**​**](https://docs.kyberswap.com/explanation/peripheral-base-contracts#input-1)

| Type                                                                                   | Explanation                                |
| -------------------------------------------------------------------------------------- | ------------------------------------------ |
| [`AddLiquidityParams`](elastic-peripheral-base-contracts.md#struct-addliquidityparams) | Parameters for addiing liquidity to a pool |

**Output**[**​**](https://docs.kyberswap.com/explanation/peripheral-base-contracts#output-1)

| Field                 | Type          | Explanation                                       |
| --------------------- | ------------- | ------------------------------------------------- |
| `liquidity`           | `uint128`     | amount of liquidity added                         |
| `amount0`             | `uint256`     | amount of token0 required                         |
| `amount1`             | `uint256`     | amount of token1 required                         |
| `feeGrowthInsideLast` | `uint256`     | latest feeGrowthInsideLast calculated by the pool |
| `pool`                | `IProAMMPool` | pool address                                      |

### `_callbackData()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#\_callbackdata) <a href="#_callbackdata" id="_callbackdata"></a>

Function to encode input parameters to CallbackData

| Input Field | Type      | Explanation              |
| ----------- | --------- | ------------------------ |
| `token0`    | `address` | first token of the pool  |
| `token1`    | `address` | second token of the pool |
| `fee`       | `uint16`  | the pool's swap fee      |

### `_getPool()`[​](https://docs.kyberswap.com/explanation/peripheral-base-contracts#\_getpool) <a href="#_getpool" id="_getpool"></a>

Function for computing the pool address with the given input parameters.

| Input Field | Type      | Explanation              |
| ----------- | --------- | ------------------------ |
| `token0`    | `address` | first token of the pool  |
| `token1`    | `address` | second token of the pool |
| `fee`       | `uint16`  | the pool's swap fee      |
