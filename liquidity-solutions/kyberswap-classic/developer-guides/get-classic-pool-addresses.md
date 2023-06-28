---
description: Uncover The Best Pools
---

# Get Classic Pool Addresses

## Overview[​](https://docs.kyberswap.com/Classic/contract/fetching-pool-addresses#overview) <a href="#overview" id="overview"></a>

For each token pair, there are possibly many multiple pools with different configurations. As such, it is necessary to specify which pools are to be used for fetching token rates, trade execution and liquidity provision.

### getPools[​](https://docs.kyberswap.com/Classic/contract/fetching-pool-addresses#getpools) <a href="#getpools" id="getpools"></a>

The best way to get all pools for a specific token pair is to call [getPools](https://docs.kyberswap.com/reference/smart-contract/factory#getpools) on the factory, then selecting one of the pools from the returned array. If none exists, an empty array is returned.

```solidity
address[] memory poolAddresses = dmmFactory.getPools(usdt, dai);
```

## Selecting the right pool[​](https://docs.kyberswap.com/Classic/contract/fetching-pool-addresses#selecting-the-right-pool) <a href="#selecting-the-right-pool" id="selecting-the-right-pool"></a>

Given a token pair, the KyberSwap website will show the unamplified pool and those created by the Kyber team.

### Unamplified Pool[​](https://docs.kyberswap.com/Classic/contract/fetching-pool-addresses#unamplified-pool) <a href="#unamplified-pool" id="unamplified-pool"></a>

For direct smart contract integrations, the unamplified pool (amplification factor 1) is recommended for simplicity. This pool supports an infinite price range, and therefore should always have liquidity. The pool address can be fetched by calling getUnamplifiedPool on the factory.

```solidity
address poolAddress = dmmFactory.getUnamplifiedPool(usdt, dai);
```

### Pool with best liquidity[​](https://docs.kyberswap.com/Classic/contract/fetching-pool-addresses#pool-with-best-liquidity) <a href="#pool-with-best-liquidity" id="pool-with-best-liquidity"></a>

An alternative method is to call the factory's [getPools](get-classic-pool-addresses.md#getpools) method to fetch all pools for the token pair, then sorting by liquidity.

This can be done by fetching each pool's kLast method, then whichever pool has the highest `kLast` value should be used. We provide a short code snippet below.

```solidity
address[] memory poolAddresses = dmmFactory.getPools(usdt, dai);
address bestPool;
uint256 highestKLast = 0;
uint256 bestIndex = 0;
for (uint i = 0; i < poolAddresses.length; i++) {
    uint256 currentKLast = IDMMPool(poolAddresses[i]).kLast();
    if (currentKLast > highestKLast) {
        highestKLast = currentKLast;
        bestIndex = i;
    }
}
// handle case if highestKLast is 0 (no liquidity)
if (highestKLast == 0) {
    bestPool = address(0);
} else {
    bestPool = poolAddresses[bestIndex];
}

// use bestPool for rate queries, liquidity provision or swaps
```

To save on gas costs, this process is recommended to be performed off-chain, then have the pool address(es) specified as an input. See the first method in the example below.

## Example[​](https://docs.kyberswap.com/Classic/contract/fetching-pool-addresses#example) <a href="#example" id="example"></a>

We showcase 3 methods for getting pool addresses to calculate the USDT amount needed to obtain 100 DAI.

Note that we import the [router](https://github.com/KyberNetwork/dmm-smart-contracts/blob/master/contracts/interfaces/IDMMRouter02.sol) and [factory](https://github.com/KyberNetwork/dmm-smart-contracts/blob/master/contracts/interfaces/IDMMFactory.sol) interfaces.

```solidity
pragma solidity 0.6.6;

import "./IDMMRouter02.sol";
import "./IDMMFactory.sol";


contract Example {
    IDMMRouter02 public dmmRouter;
    IDMMFactory public dmmFactory;
    IERC20 public usdt = 0xdac17f958d2ee523a2206206994597c13d831ec7; // mainnet USDT address
    IERC20 public dai = '0x6b175474e89094c44da98b954eedeac495271d0f'; // mainnet DAI address
    IERC20[] public tokensPath = [usdt,dai];

    constructor(IDMMRouter02 _dmmRouter) {
        dmmRouter = _dmmRouter;
        dmmFactory = IDMMFactory(dmmRouter.factory());
    }

    // the first (and our recommended) method is to
    // query for the best pool off-chain and pass it as an input
    function getRateFirstMethod(address[] poolsPath) external view returns (uint256[] amounts) {
        // return amounts
        return dmmRouter.getAmountsIn(
            1e20, // 100 DAI
            poolsPath,
            tokensPath
        );
    }

    // the second method is to use the unamplified pool
    // while convenient, it may not be optimal
    function getRateSecondMethod() external view returns (uint256[] amounts) {
        address poolAddress = dmmFactory.getUnamplifiedPool(usdt, dai);

        // use unamplified pool
        addresss[] memory poolsPath = new address[](1);
        poolsPath[0] = poolAddress;

        // return amounts
        return dmmRouter.getAmountsIn(
            1e20, // 100 DAI
            poolPath,
            tokensPath
        );
    }

    // the third method is to use the pool found in the first index of the pool array
    // if no pools are available, return empty array
    function getRateThirdMethod() external view returns (uint256[] amounts) {
        address[] memory poolAddresses = dmmFactory.getPools(usdt, dai);
        if (poolAddresses.length == 0) return;

        // use the pool address of the first index of the pool array
        addresss[] memory poolsPath = new address[](1);
        poolsPath[0] = poolAddresses[0];

        // return amounts
        return dmmRouter.getAmountsIn(
            1e20, // 100 DAI
            poolPath,
            tokensPath
        );
    }
}
```
