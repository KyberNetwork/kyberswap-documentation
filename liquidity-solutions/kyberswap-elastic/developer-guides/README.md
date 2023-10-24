---
description: Code Samples To Get You Started
---

# Developer Guides

The guides in the following section are targeted at application developers as well as smart contract integrators that are interested in building on top of the KyberSwap Elastic ecosystem.

{% hint style="success" %}
**Elastic SDK**

KyberSwap has created an [Elastic SDK](https://github.com/KyberNetwork/ks-sdk-elastic) to make interacting with our Elastic smart contracts easier. You can refer to our [Elastic SDK Developer Guides](../../elastic-sdk/developer-guides/) for step-by-step walkthroughs on how to achieve various Elastic operations in a TypeScript environment.
{% endhint %}

## Project bootstrapping

Given the composability of DeFi protocols, we recommend using Hardhat's [mainnet forking feature](https://hardhat.org/guides/mainnet-forking.html) to best stimulate mainnet conditions. This will enable integrations to be conveniently tested against existing protocols without having to bootstrap each and every protocol individually.

## Overview

KyberSwap Elastic consists of multiple smart contracts, each having been deliberately confined to a specific function. If you would like to view the full list of contracts as well as their respective functions and variables, the contracts have been split according to the below:

* [**Core Contracts:**](../contracts/elastic-core-contracts.md) Handles all pool functionalities, including the creation of the pool
* [**Core Libraries:**](../contracts/elastic-core-libraries.md) Contains deployment contracts as well as multiple math contracts for safe handling of numbers.
* [**Periphery Core Contracts:**](../contracts/elastic-periphery-core-contracts.md) Contracts which handle swap routing as well as management of liquidity positions.
* [**Peripheral Library Contracts:**](../contracts/elastic-peripheral-library-contracts.md) Contains the anti-sniping contract as well as various contracts to aid data queries.
* [**Peripheral Base Contracts:**](../contracts/elastic-peripheral-base-contracts.md) Helper contracts that process, validate, and store peripheral liquidity flows.

The contracts that are of particular interest are listed below:

* [**Factory:**](../contracts/elastic-core-contracts.md#factory) Handles deployment of Kyberswap Elastic pools and where administrative configurations are held, such as the whitelisting of NFT position managers, and government fee settings.
* [**Router:**](../contracts/elastic-periphery-core-contracts.md#router) Handles the routing of swaps across an Elastic pool.
* QouterV2: Allows getting the expected amount out or amount in for a given swap without executing the swap.
* [**AntiSnipAttackPositionManager:**](../contracts/elastic-periphery-core-contracts.md#antisnipattackpositionmanager) Adds the anti-sniping attack feature to the liquidity additions or removals.
* TicksFeeReader: Handles the management of ticks as well as the corresponding positions and fees.
* TokenPositionDescriptor: Enables querying of position information.
* TokenPositionDescriptionProxy: An ERC1967 contract that implements an upgradeable proxy for the TokenPositionDescriptor contract.

Please refer to [Elastic Contract Addresses](../contracts/elastic-contract-addresses.md) for the full list of contracts which have been deployed across the supported chains.

## Next steps

As there are possibly multiple pools per token pair, the first step is to [fetch pool addresses](get-elastic-pool-addresses.md) and determine which pool is most suitable for querying swap rates, trade execution and liquidity provision.

Traders and arbitrageurs who need to take liquidity should view the section on [swap execution](execute-an-elastic-swap.md).
