---
description: Code Samples To Get You Started
---

# Developer Guides

The guides in the following section are targeted at application developers as well as smart contract integrators that are interested in building on top of the KyberSwap Classic ecosystem.

## Project bootstrapping

Given the composability of DeFi protocols, we recommend using Hardhat's [mainnet forking feature](https://hardhat.org/guides/mainnet-forking.html) to best stimulate mainnet conditions. This will enable integrations to be conveniently tested against existing protocols without having to bootstrap each and every protocol individually.

## Overview

KyberSwap Classic implements two smart contract variants that correspond to the fee setting for the pool as the fee logic differs significantly between the two. The contract variants are differentiated based on the smart contract name prefix whereby:

* `KS`: KyberSwap Classic with static fees
* `DMM`: KyberSwap Classic with dynamic fees

In terms of contracts, there are two contracts of particular interest: `Router` and `Factory`. The different contracts and their purposes are listed below:

* `Router`: Handles the core flows which includes liquidity provision, token rate queries, and token swap execution.
* `Factory`: Contract that eables the creation of KyberSwap Classic pools.
* `ZapIn`: Enable users to zap into and out of the pool.
* `Multicall`: Ensures data synchronization by aggregating multiple smart contract function calls into a single call.

Please refer to [Classic Contract Addresses](../contracts/classic-contract-addresses.md) for the full list of contracts which have been deployed across the supported chains.

## Next Steps

As there are possibly multiple pools per token pair, the first step is to [fetch pool addresses](get-classic-pool-addresses.md) and determine which pool is most suitable for querying swap rates, trade execution and liquidity provision.

Traders and arbitrageurs who need to take liquidity should view the section on [swap execution](execute-a-classic-swap.md).

The section on [providing liquidity](providing-liquidity-to-classic-pools.md) will guide liquidity providers through the process of adding and removing liquidity.
