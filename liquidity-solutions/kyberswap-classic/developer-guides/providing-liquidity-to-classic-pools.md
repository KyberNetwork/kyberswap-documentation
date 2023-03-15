---
description: Add/Remove Liquidity From Classic Pools
---

# Providing Liquidity To Classic Pools

## Pool creation

In some cases, your contract may be instantiating a new pool for a token pair. This can be done by calling the router's createPool function.

### Example[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#example) <a href="#example" id="example"></a>

Create a new DAI-USDC pool with amplification factor of 50. Refer to [this section](../concepts/dynamic-pricing-curves.md) to understand more about the amplification factor.

```solidity
poolAddress = dmmFactory.createPool(dai, usdc, 50000);
```

Kindly note the following:

* The token addresses are interchangeable, ie. `dmm.createPool(usdc, dai, 50000)` yields the same result.
* There can be at most 1 unamplified pool for a token pair, ie. only 1 pool can exist with `ampBps = BPS (10000)`. Should there already be an existing unamplified pool, attempts to create another one will fail.

## Adding liquidity

To safely add liquidity to a pool, we recommend using the router. There are different functions for adding liquidity to existing pools or creating a new pool, and if the token pair is ERC20-ERC20, or ETH-ERC20.

These methods both require committment to a _belief about the current price_, which is encoded in the `amount*Desired` parameters. While it is fairly safe to assume that the current fair market price is around what the current reserve ratio is for a pair due to arbitrage, it is dangerous to obtain this ratio within the same transaction as it can be easily manipulated.

In addition, the `amount*Min` and `vReserveRatioBounds` parameters should be utilised as a sanity buffer as the market price may shift drastically before the transaction is confirmed.

### Determining the appropriate pool[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#determining-the-appropriate-pool) <a href="#determining-the-appropriate-pool" id="determining-the-appropriate-pool"></a>

See [this section](get-classic-pool-addresses.md) on pool selection.

### Examples[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#examples) <a href="#examples" id="examples"></a>

1. Create a new ERC20-ERC20 pool with amplification factor 100
2. Add liquidity to an existing ERC20-ERC20 with FoT pool

Creation and liquidity provision to ERC20-ETH pools are similar, with the only difference being the functions to be called.

### New ERC20-ERC20 pool via addLiquidityNewPool[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#new-erc20-erc20-pool-via-addliquiditynewpool) <a href="#new-erc20-erc20-pool-via-addliquiditynewpool" id="new-erc20-erc20-pool-via-addliquiditynewpool"></a>

For new ERC20-ETH pool creations, the equivalent function is addLiquidityNewPoolETH.

**Example: Create a new pool with 100 USDC and 100 USDT**[**​**](https://docs.kyberswap.com/Classic/contract/providing-liquidity#example-create-a-new-pool-with-100-usdc-and-100-usdt)

```solidity
// Note: assume that usdc and usdt token approvals have been given to router
// and that transferFrom has been called to transfer tokens to contract from user
dmmRouter.addLiquidityNewPool(
    usdc,
    usdt,
    1000000, // amplification factor of 100
    100 * 1e6, // 100 usdc
    100 * 1e6, // 100 usdt
    100 * 1e6, // no slippage tolerance because it is a new pool
    100 * 1e6 // no slippage tolerance because it is a new pool
);
```

### Add to existing ERC20-ERC20 (FoT) pool via addLiquidity[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#add-to-existing-erc20-erc20-fot-pool-via-addliquidity) <a href="#add-to-existing-erc20-erc20-fot-pool-via-addliquidity" id="add-to-existing-erc20-erc20-fot-pool-via-addliquidity"></a>

Although CORE is a Fee-on-Transfer (FoT) token, it utilises the same function as adding liquidity to an existing ERC20-ERC20 pool. However, it is likely that the slippage tolerance will have to be adjusted to account for the token fee.

For adding liquidity to existing ERC20-ETH pools, the the equivalent function is addLiquidityETH.

**Example: Add 1 CORE and 1000 USDT**[**​**](https://docs.kyberswap.com/Classic/contract/providing-liquidity#example-add-1-core-and-1000-usdt)

```solidity
// Note: assume that core and usdt token approvals have been given to router
// and that transferFrom has been called to transfer tokens to contract from user

// the vReserveRatioBounds below is set to the absolute minimum and maximum values as an example
// it is recommended to read the virtual reserve ratio and set the appropriate values from that
vReserveRatioBounds = new uint256[2];
(vReserveRatioBounds[0], vReserveRatioBounds[1]) = (0, -1);
dmmRouter.addLiquidity(
    core,
    usdt,
    core-usdt-pool, // core-usdt pool address
    1 * 1e18, // 1 core
    1000 * 1e6, // 1000 usdt
    97 * 1e16, // 3% slippage tolerance (0.97 core / 1000 usdt)
    970 * 1e6, // 3% slippage tolerance (1 core / 970 usdt)
    vReserveRatioBounds
);
```

## Removing liquidity

As is the case with Uniswap LP tokens, DMM-LP tokens implement meta-approvals to vastly help improve UX and save on gas costs. Hence, we recommend the usage of the `removeLiquidity*withPermit*` functions.

### Removing LP tokens from ERC20-ERC20 pool[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#removing-lp-tokens-from-erc20-erc20-pool) <a href="#removing-lp-tokens-from-erc20-erc20-pool" id="removing-lp-tokens-from-erc20-erc20-pool"></a>

#### Removing 100 wbtc-usdt LP tokens via removeLiquidityWithPermit[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#removing-100-wbtc-usdt-lp-tokens-via-removeliquiditywithpermit) <a href="#removing-100-wbtc-usdt-lp-tokens-via-removeliquiditywithpermit" id="removing-100-wbtc-usdt-lp-tokens-via-removeliquiditywithpermit"></a>

Note: For FoT tokens like CORE, the same function can be used, but the minimum receivable of core tokens should be adjusted.

```solidity
dmmRouter.removeLiquidityWithPermit(
    wbtc,
    usdt,
    wbtc-usdt-pool, // wbtc-usdt pool address
    100 * 1e8, // 100 wbtc-usdt LP tokens
    1 * 1e8, // Min receivable of 1 wbtc
    100 * 1e6, // Min receivable of 100 usdt
    msg.sender, // send assets to msg.sender
    block.timestamp, // deadline
    approveMax, // boolean flag if max token allowance approval
    v, // approve permit signature field
    r, // approve permit signature field
    s // approve permit signature field
);
```

### Removing LP tokens from ERC20-ETH pool[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#removing-lp-tokens-from-erc20-eth-pool) <a href="#removing-lp-tokens-from-erc20-eth-pool" id="removing-lp-tokens-from-erc20-eth-pool"></a>

#### Removing 100 core-eth LP tokens via removeLiquidityETHWithPermitSupportingFeeOnTransferTokens[​](https://docs.kyberswap.com/Classic/contract/providing-liquidity#removing-100-core-eth-lp-tokens-via-removeliquidityethwithpermitsupportingfeeontransfertokens) <a href="#removing-100-core-eth-lp-tokens-via-removeliquidityethwithpermitsupportingfeeontransfertokens" id="removing-100-core-eth-lp-tokens-via-removeliquidityethwithpermitsupportingfeeontransfertokens"></a>

```solidity
dmmRouter.removeLiquidityETHWithPermitSupportingFeeOnTransferTokens(
    core,
    core-eth-pool, // core-eth pool address
    100 * 1e8, // 100 core-eth LP tokens
    1 * 1e18, // Min receivable of 1 core
    10 * 1e17, // Min receivable of 0.1 ether
    msg.sender, // send assets to msg.sender
    block.timestamp, // deadline
    approveMax, // boolean flag if max token allowance approval
    v, // approve permit signature field
    r, // approve permit signature field
    s // approve permit signature field
);
```
