---
description: Trade Directly Against A Classic Pool
---

# Execute A Classic Swap

## Using the router

We recommend using the router for swapping to and from different assets, which has different swapping functions for ETH, tokens, and tokens that have fee-on-transfer features.

Before executing the swap, it is recommended that an external price source is used to fix the minimum output tokens receivable when selling a fixed amount of tokens, or maximum amount of input tokens to be used when purchasing a fixed amount of tokens.

Your smart contract should also:

1. Have enough ETH and/or tokens when executing the swap
2. Be able to receive ETH, when it is the destination address for swapping to ETH
3. Have granted approval to the router when swapping from tokens

## Obtaining pool addresses

It is necessary to specify which pools are to be used for the token swap. Read more about [fetching pool addresses](get-classic-pool-addresses.md) before proceeding.

Since each pool represents a token pair, it stands to be the case that the `poolsPath` specified for token swaps must be 1 size smaller than `path`, ie. `poolsPath.length = path.length - 1`. Refer to the examples below.

## Examples

We will cover 3 scenarios:

1. Swap 1 ETH for DAI
2. Swap USDC to obtain 1 ETH, with WBTC as an intermediary
3. Swap 1 CORE (fee-on-transfer token) for USDT

### 1 ETH -> DAI[​](https://docs.kyberswap.com/Classic/contract/swap-execution#1-eth---dai) <a href="#1-eth---dai" id="1-eth---dai"></a>

#### swapExactEthForTokens[​](https://docs.kyberswap.com/Classic/contract/swap-execution#swapexactethfortokens) <a href="#swapexactethfortokens" id="swapexactethfortokens"></a>

A common error when swapping from ETH is forgetting to actually send ETH when calling the function. The `value` field should match the amount of ETH sent.

```solidity
IERC20[] memory path = new address[](2);
path[0] = dmmRouter.weth();
path[1] = dai; // assuming dai is specified as IERC20
// value = 1 ETH, alternatively use msg.value
dmmRouter.swapExactEthForTokens{value: 1e18}(
    amountOutMin, // should be obtained via a price oracle, either off or on-chain
    poolsPath, // eg. [eth-dai-pool]
    path,
    msg.sender,
    block.timestamp
);
```

### USDC -> WBTC -> 1 ETH[​](https://docs.kyberswap.com/Classic/contract/swap-execution#usdc---wbtc---1-eth) <a href="#usdc---wbtc---1-eth" id="usdc---wbtc---1-eth"></a>

#### Transferring tokens[​](https://docs.kyberswap.com/Classic/contract/swap-execution#transferring-tokens) <a href="#transferring-tokens" id="transferring-tokens"></a>

Before swapping, the contract should be in possession of USDC. The caller can either send the tokens beforehand, or give allowance to the contract to call the `transferFrom` method. The short code snippet below showcases the latter.

```solidity
uint256 amountIn = 50 * 10 ** usdc.decimals();
require(usdc.transferFrom(msg.sender, address(this), amountIn), 'transferFrom failed');
```

#### Granting Approval[​](https://docs.kyberswap.com/Classic/contract/swap-execution#granting-approval) <a href="#granting-approval" id="granting-approval"></a>

The next step is then to give the router some USDC allowance.

```solidity
require(usdc.approve(address(dmmRouter), amountIn), 'approve failed');
```

#### `path` and `poolsPath`[​](https://docs.kyberswap.com/Classic/contract/swap-execution#path-and-poolspath) <a href="#path-and-poolspath" id="path-and-poolspath"></a>

Since the intended token path is usdc -> wbtc -> eth, `path = [usdc, wbtc, weth]`. We also need to specify the usdc-wbtc and wbtc-eth pools to be used. Deciding which pools to use can be found in [this](get-classic-pool-addresses.md) section. Eg. `poolsPath=[usdc-wbtc-pool, wbtc-weth-pool]`, where `usdc-wbtc-pool` and `wbtc-weth-pool` are the pool addresses to be used.

#### swapExactTokensForETH[​](https://docs.kyberswap.com/Classic/contract/swap-execution#swapexacttokensforeth) <a href="#swapexacttokensforeth" id="swapexacttokensforeth"></a>

Note that if the destination address is a contract, it should have the `receive() external payable { ... }` or fallback function declaration in order to receive ETH.

```solidity
IERC20[] memory path = new address[](3);
path[0] = usdc; // assuming usdc is specified as IERC20
path[1] = wbtc; // assuming wbtc is specified as IERC20
path[2] = dmmRouter.weth();
dmmRouter.swapExactTokensForEth(
    amountOutMin, // should be obtained via a price oracle, either off or on-chain
    poolsPath, // eg. [usdc-wbtc-pool, wbtc-weth-pool]
    path,
    msg.sender, // has to be able to receive ETH
    block.timestamp
);
```

### 1 CORE -> USDT[​](https://docs.kyberswap.com/Classic/contract/swap-execution#1-core---usdt) <a href="#1-core---usdt" id="1-core---usdt"></a>

This example is similar to the previous example of USDC -> WBTC -> ETH. The only exception is that CORE is a fee-on-transfer token, and thus requires special handling.

#### swapExactTokensForTokensSupportingFeeOnTransferTokens[​](https://docs.kyberswap.com/Classic/contract/swap-execution#swapexacttokensfortokenssupportingfeeontransfertokens) <a href="#swapexacttokensfortokenssupportingfeeontransfertokens" id="swapexacttokensfortokenssupportingfeeontransfertokens"></a>

We assume that the previous steps of transferring tokens and token approval to the router has been performed.

```solidity
IERC20[] memory path = new address[](2);
path[0] = core; // assuming core is specified as IERC20
path[1] = usdt; // assuming usdt is specified as IERC20
dmmRouter.swapExactTokensForTokensSupportingFeeOnTransferTokens(
    amountOutMin, // should be obtained via a price oracle, either off or on-chain
    poolsPath, // eg. [core-usdt-pool]
    path,
    msg.sender,
    block.timestamp
);
```
