---
description: Linking Blockchains To The World
---

# Oracles

## Overview

Much like how we rely on our senses to make sense of the world around us, blockchains require an interface to receive data that is external to their own chain. Data on the blockchain (i.e. [on-chain data](on-chain-vs-off-chain-data.md)) can be easily consumed for on-chain functions but is limited to data which can be fully-described by the blockchain. In other words, blockchains are unable to access data that is stored outside the blockchain network (i.e. [off-chain data](on-chain-vs-off-chain-data.md)). As such, blockchains require an oracle to feed off-chain data so that it can be used for on-chain processing by smart contracts. In effect, oracles function as a bridge between the blockchain and all external data sources.

The most relatable example in DeFi is that of fiat-backed [stablecoins](../decentralized-finance/stablecoins.md), whereby every unit of USDC is backed by the equivalent cash amount held in a bank account. As the blockchain does not have access to the bank account, it relies on a trusted party to feed the data into the blockchain so that the on-chain token balances can be adjusted according to the off-chain cash balances. In this case, USDC users entrusts this oracle function to [Circle](https://www.circle.com/en/about-circle), which operates the USDC token.&#x20;

Note that as off-chain data is not determined by the network, all oracles require some form of trust assumption when it comes to identifying a source of truth. This can range from a single entity who is the sole owner of the source of truth or complex game theoretical models which enable consensus to be reached. In the latter case, the oracle design becomes extremely important as economic incentives must be aligned with data correctness. Given that the data from oracles will likely be used to trigger some form of on-chain computation, the reliability and security of the oracle data feed is paramount to ensure that the robustness of the ecosystem as a whole.

{% tabs %}
{% tab title="Developers" %}
* [Get Elastic Pool Price](../../../liquidity-solutions/kyberswap-elastic/developer-guides/get-elastic-pool-price.md)
{% endtab %}
{% endtabs %}
