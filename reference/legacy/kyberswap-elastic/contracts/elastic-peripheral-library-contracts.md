# Elastic Peripheral Library Contracts

## AntiSnipingAttack[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#antisnipingattack) <a href="#antisnipingattack" id="antisnipingattack"></a>

The motivation and explanation of the mechanism can be found [here](https://docs.google.com/document/d/1F50RWQRRyaNxnW5RvKgw09fN2FofIVLVccijgcOt-Iw/edit#heading=h.trv8zmis8u4c). The function containing the bulk of the logic is [`update()`](elastic-peripheral-library-contracts.md#update).

### Struct: Data[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#struct-data) <a href="#struct-data" id="struct-data"></a>

| Field            | Type     | Formula Variable | Explanation                         |
| ---------------- | -------- | ---------------- | ----------------------------------- |
| `lastActionTime` | `uint32` | $$t_{last}$$     | timestamp of last action performed  |
| `lockTime`       | `uint32` | $$t_{lock}$$     | average start time of lock schedule |
| `unlockTime`     | `uint32` | $$t_{unlock}$$   | average unlock time of locked fees  |
| `feesLocked`     | `uint32` | $$fee_{locked}$$ | locked rToken qty since last update |

### `initialize()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#initialize) <a href="#initialize" id="initialize"></a>

Initializes [Data](elastic-peripheral-library-contracts.md#struct-data) values for a new position. The time variables are set to the current timestamp, while `feesLocked` is set to zero.

### `update()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#update) <a href="#update" id="update"></a>

Updates [Data](elastic-peripheral-library-contracts.md#struct-data) values for an existing position. Calculates the amount of claimable reinvestment tokens to be sent to the user and, in the case of liquidity removal, the amount of burnable reinvestment tokens as well.

**Formula**[**​**](https://docs.kyberswap.com/explanation/peripheral-library-contracts#formula)

$$claimBps_{new} = min(BPS, \frac{t_{now}-t_{lock}}{t_{target}})$$&#x20;

$$claimBps_{current} = min(BPS, \frac{t_{now}-t_{last}}{t_{unlock} - t_{target}})$$&#x20;

if $$t_{unlock} > t_{target}$$, $$BPS$$ otherwise $$fee_{harvest}$$ and $$fee_{lock}$$ updated through [`calcFeeProportions()`](https://docs.kyberswap.com/explanation/peripheral-library-contracts#calcFeeProportions)&#x20;

$$t_{unlock} = \frac{(t_{lock} + t_{target}) * (BPS - claimBps_{new}) * fee_{collect} + t_{unlock} * (BPS - claimBps_{current}) * fee_{locked}}{fee_{lock} * BPS}$$

* If adding liquidity, update $$t_{lock} = ceil(\frac{max(t_{lock}, t_{now} - t_{target})*L + t_{now} * \Delta{L}}{L + \Delta{L}})$$
* If removing liquidity,
  * $$fee_{burn} = fee_{harvest} * \frac{\Delta{L}}{L}$$
  * $$fee_{harvest}$$ -= $$fee_{burn}$$

**Input**[**​**](https://docs.kyberswap.com/explanation/peripheral-library-contracts#input)

<table><thead><tr><th>Field</th><th width="156">Type</th><th width="171">Formula Variable</th><th>Explanation</th></tr></thead><tbody><tr><td><code>self</code></td><td><a href="elastic-peripheral-library-contracts.md#struct-data"><code>Data</code></a></td><td>N.A.</td><td>stored data values for an existing position</td></tr><tr><td><code>currentLiquidity</code></td><td><code>uint128</code></td><td><span class="math">L</span></td><td>current position liquidity</td></tr><tr><td><code>liquidityDelta</code></td><td><code>uint128</code></td><td><span class="math">\Delta{L}</span></td><td>quantity change to be applied</td></tr><tr><td><code>currentTime</code></td><td><code>uint32</code></td><td><span class="math">t_{now}</span></td><td>current block timestamp</td></tr><tr><td><code>isAddLiquidity</code></td><td><code>bool</code></td><td>N.A.</td><td>true = add liquidity, false = remove liquidity</td></tr><tr><td><code>feesSinceLastAction</code></td><td><code>uint256</code></td><td><span class="math">fee_{collect}</span></td><td>fees accrued since last action</td></tr><tr><td><code>vestingPeriod</code></td><td><code>uint256</code></td><td><span class="math">t_{target}</span></td><td>maximum time duration for which LP fees are proportionally burnt upon LP removals</td></tr></tbody></table>

**Output**[**​**](https://docs.kyberswap.com/explanation/peripheral-library-contracts#output)

| Field           | Type      | Formula Variable  | Explanation                         |
| --------------- | --------- | ----------------- | ----------------------------------- |
| `feesClaimable` | `uint256` | $$fee_{harvest}$$ | claimable reinvestment token amount |
| `feesBurnable`  | `uint256` | $$fee_{burn}$$    | reinvestment token amount to burn   |

### `calcFeeProportions()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#calcfeeproportions) <a href="#calcfeeproportions" id="calcfeeproportions"></a>

Calculates the proportion of locked fees and claimable fees given the fee amounts and claimable fee basis points.

**Formula**[**​**](https://docs.kyberswap.com/explanation/peripheral-library-contracts#formula-1)

$$fee_{harvest} = \frac{claimBps_{current}}{BPS} * fee_{locked} + \frac{claimBps_{new}}{BPS} * fee_{collect}$$ $$fee_{lock} = fee_{locked} + fee_{collect} - fee_{harvest}$$

**Input**[**​**](https://docs.kyberswap.com/explanation/peripheral-library-contracts#input-1)

<table><thead><tr><th width="217">Field</th><th width="158">Type</th><th width="170">Formula Variable</th><th>Explanation</th></tr></thead><tbody><tr><td><code>currentFees</code></td><td><code>uint256</code></td><td><span class="math">fee_{locked}</span></td><td>currently locked fees</td></tr><tr><td><code>nextFees</code></td><td><code>uint256</code></td><td><span class="math">fee_{collect}</span></td><td>fees since last action</td></tr><tr><td><code>currentClaimableBps</code></td><td><code>uint256</code></td><td><span class="math">claimBps_{current}</span></td><td>proportion of claimable / unlocked <code>currentFees</code> in basis points</td></tr><tr><td><code>nextClaimableBps</code></td><td><code>uint256</code></td><td><span class="math">claimBps_{new}</span></td><td>proportion of claimable <code>nextFees</code> in basis points</td></tr></tbody></table>

**Output**[**​**](https://docs.kyberswap.com/explanation/peripheral-library-contracts#output-1)

<table><thead><tr><th width="187">Field</th><th width="112">Type</th><th width="157">Formula Variable</th><th>Explanation</th></tr></thead><tbody><tr><td><code>feesLockedNew</code></td><td><code>uint256</code></td><td><span class="math">fee_{lock}</span></td><td>new fee amount to be locked</td></tr><tr><td><code>feesClaimable</code></td><td><code>uint256</code></td><td><span class="math">fee_{harvest}</span></td><td>claimable fees to be sent to user</td></tr></tbody></table>

## BytesLib[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#byteslib) <a href="#byteslib" id="byteslib"></a>

Solidity Bytes Arrays Utils @author Gonçalo Sá [goncalo.sa@consensys.net](mailto:goncalo.sa@consensys.net)&#x20;

Bytes tightly packed arrays utility library for ethereum contracts written in Solidity. The library lets you slice and type cast bytes arrays both in memory and storage.

## LiquidityMath[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#liquiditymath) <a href="#liquiditymath" id="liquiditymath"></a>

Contract to calculate the expected amount of **liquidity** given the amounts of tokens.

### `getLiquidityFromQty0()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#getliquidityfromqty0) <a href="#getliquidityfromqty0" id="getliquidityfromqty0"></a>

```
Params:
    uint160 lowerSqrtP     // a lower sqrt price of the position
    uint160 upperSqrtP     // a upper sqrt price of the position
    uint256 qty0           // the amount of token0 to add
Returns:
    uint128 liquidity       // amount of liquidity to receive
```

Get liquidity from **qty0** of the first token given the price range.

### `getLiquidityFromQty1()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#getliquidityfromqty1) <a href="#getliquidityfromqty1" id="getliquidityfromqty1"></a>

```
Params:
    uint160 lowerSqrtP     // a lower sqrt price of the position
    uint160 upperSqrtP     // a upper sqrt price of the position
    uint256 qty1           // the amount of token1 to add
Returns:
    uint128 liquidity       // amount of liquidity to receive
```

Get liquidity from **qty1** of the second token given the price range.

### `getLiquidityFromQties()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#getliquidityfromqties) <a href="#getliquidityfromqties" id="getliquidityfromqties"></a>

```
Params:
    uint160 currentSqrtP    // the current price, e.g the pool's current price
    uint160 lowerSqrtP      // a lower sqrt price of the position
    uint160 upperSqrtP      // a upper sqrt price of the position
    uint256 qty0            // the amount of token0 to add
    uint256 qty1            // the amount of token1 to add
Returns:
    uint128 liquidity       // amount of liquidity to receive
```

Get liquidity given the price range and amounts of 2 tokens

## PathHelper[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#pathhelper) <a href="#pathhelper" id="pathhelper"></a>

Functions for manipulating path data for multihop swaps

### Variables[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#variables) <a href="#variables" id="variables"></a>

```
ADDR_SIZE = 20 // length of the address, i.e 20 bytes
FEE_SIZE = 2 // length of the fee, i.e 2 bytes
TOKEN_AND_POOL_OFFSET = ADDR_SIZE + FEE_SIZE// the offset of a single token address + pool fee
POOL_DATA_OFFSET = TOKEN_AND_POOL_OFFSET + ADDR_SIZE // the offset of 2 token addresses + pool fee
MULTIPLE_POOLS_MIN_LENGTH = POOL_DATA_OFFSET + TOKEN_AND_POOL_OFFSET // min length that contains at least 2 pools
```

### `hasMultiplePools()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#hasmultiplepools) <a href="#hasmultiplepools" id="hasmultiplepools"></a>

```
Params:
    bytes path
Returns:
    bool
```

Return true if the path contains 2 or more pools, false otherwise

### `numPools()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#numpools) <a href="#numpools" id="numpools"></a>

```
Params:
    bytes path
Returns:
    uint256
```

Returns the number of pools in the path.

### `decodeFirstPool()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#decodefirstpool) <a href="#decodefirstpool" id="decodefirstpool"></a>

```
Params:
    bytes path
Returns:
    address tokenA
    address tokenB
    uint16 fee
```

Return the first pool's data from the **path**, including **tokenA**, **tokenB** and **fee**.

### `getFirstPool()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#getfirstpool) <a href="#getfirstpool" id="getfirstpool"></a>

```
Params:
    bytes path
Returns:
    bytes data
```

Return the segment corresponding to the first pool in the path.

### `skipToken()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#skiptoken) <a href="#skiptoken" id="skiptoken"></a>

```
Params:
    bytes path
Returns:
    bytes newPath
```

Skip a token + fee from the buffer and returns the remainder.

## PoolAddress[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#pooladdress) <a href="#pooladdress" id="pooladdress"></a>

Provides a function for deriving a pool address from the factory, tokens, and swap fee

### `computeAddress()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#computeaddress) <a href="#computeaddress" id="computeaddress"></a>

```
Params:
    address factory   // DMMv2 factory contract
    address token0    // the first token of the pool
    address token1    // the second token of the pool
    uint16 swapFee    // the fee of the pool
    bytes32 poolInitHash    // the keccake256 hash of the Pool creation code
Returns:
    address pool    // the pool address
```

Deterministically computes the pool address from the given data.

## PoolTicksCounter[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#pooltickscounter) <a href="#pooltickscounter" id="pooltickscounter"></a>

### `countInitializedTicksCrossed()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#countinitializedtickscrossed) <a href="#countinitializedtickscrossed" id="countinitializedtickscrossed"></a>

```
Params:
    IProAMMPool
    int24 nearestCurrentTickBefore
    int24 nearestCurrentTickAfter
Returns:
    uint32 initializedTicksCrossed
```

Count the number of initialized ticks have been crossed given the previous/current nearest initialized ticks to the current tick.

## TokenHelper[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#tokenhelper) <a href="#tokenhelper" id="tokenhelper"></a>

A helper contract to transfer token/ETH.

### `transferToken()`[​](https://docs.kyberswap.com/explanation/peripheral-library-contracts#transfertoken) <a href="#transfertoken" id="transfertoken"></a>

```
Params:
    IERC20 token
    uint256 amount
    address sender
    address receiver
```

Transfer an **amount** of ERC20 **token** from the **sender** to the **receiver**.

### **`transferEth()`**[**​**](https://docs.kyberswap.com/explanation/peripheral-library-contracts#transfereth)

```
Params:
    uint256 amount
    address receiver
```

Transfer an **amount** of ETH to the **receiver**.
