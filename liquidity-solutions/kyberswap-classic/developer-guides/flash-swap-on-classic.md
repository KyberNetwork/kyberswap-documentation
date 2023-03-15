# Flash Swap On Classic

The KyberSwap flash swap functionality works similarly to Uniswap's. You may read more about flash swaps [here](https://docs.uniswap.org/contracts/v2/guides/smart-contract-integration/using-flash-swaps). We highlight the syntax differences below.

### Using `dmmSwapCall`[​](https://docs.kyberswap.com/Classic/contract/flash-swaps#using-dmmswapcall) <a href="#using-dmmswapcall" id="using-dmmswapcall"></a>

```solidity
function dmmSwapCall(address sender, uint256 amount0, uint256 amount1, bytes calldata data) {
  IERC20 token0 = IDMMPool(msg.sender).token0(); // fetch the address of token0
  IERC20 token1 = IDMMPool(msg.sender).token1(); // fetch the address of token1
  assert(IDMMFactory(dmmFactory).isPool(token0, token1, msg.sender)); // ensure that caller can only be dmm pool
  // rest of the function below
}
```

## Interface

[IDMMCallee.sol](https://github.com/KyberNetwork/dmm-smart-contracts/blob/master/contracts/interfaces/IDMMCallee.sol)

```solidity
pragma solidity 0.6.6;

interface IDMMCallee {
    function dmmSwapCall(
        address sender,
        uint256 amount0,
        uint256 amount1,
        bytes calldata data
    ) external;
}
```
