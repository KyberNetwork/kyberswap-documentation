---
description: Making Sense Of Data
---

# On-Chain vs Off-Chain Data

## Overview

Unlike traditional finance where data is stored in siloed databases, DeFi transactions offers significantly greater transparency as transaction data is stored on the blockchain which can be publicly queried by any user with internet access. Critically, on-chain data is always impartial as it reflects the exact transaction parameters as it occured with no data lag nor any risks of being tampered post-transaction. The storage of data on the blockchain has become known as on-chain data with all other data sources being referred to as off-chain data.

Given that the [DeFi](../decentralized-finance/) ecosystem is powered by [dapps](dapps.md) which run on top of permissionless public blockchains, all DeFi actions results in new transaction data being created and logged on the blockchain. Moreover, with improving token standards (i.e. [ERC20](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/)) as well as DeFi smart contract best practices, DeFi transactions also emits standardized event notifications (i.e. [transfer](https://eips.ethereum.org/EIPS/eip-20#transfer-1), [swap](https://github.com/KyberNetwork/ks-classic-sc/blob/master/contracts/DMMPool.sol#L52)) which provides further context for the transaction. Consequently, there is a wealth of raw on-chain data which holds significant value once sorted.

In contrast to on-chain data, off-chain data is usually stored on a private database where access is determined by its operator. This is not inherently a bad thing as there are certain data points which can't be wholly captured by on-chain data (i.e. price, real world asset data, etc.) and such services plugs these gaps. Moreover, off-chain data providers could also provide additional value through processing raw data to uncover additional insights. This ability to make sense of raw data is both its strongest suite as well as its achilles heel as users will have to trust that the data provided is accurate.

## KyberAI: Democratizing data insights

[KyberAI](../../../kyberswap-solutions/kyberai/) was conceived with the intention of surfacing valuable market data that would empower KyberSwap users to make data-driven trades. With KyberAI, users can view both [on-chain](../../../kyberswap-solutions/kyberai/on-chain-indicators/) and [off-chain](../../../kyberswap-solutions/kyberai/technical-indicators/) data presented in user-friendly formats directly on the [KyberSwap Interface](../../../kyberswap-solutions/kyberswap-interface/). Moreover, our [KyberScore](../../../kyberswap-solutions/kyberai/kyberscore.md) model enables users to identify market opportunities all via a single number indicating the extent of a token's bullishness or bearishness.&#x20;

{% tabs %}
{% tab title="Liquidity Providers" %}
* [Deep Dive Into Token Data](../../../kyberswap-solutions/kyberai/user-guides/deep-dive-into-token-data.md)
{% endtab %}

{% tab title="Traders" %}
* [Discover Trending Tokens](../../../kyberswap-solutions/kyberai/user-guides/discover-promising-tokens.md)
* [Deep Dive Into Token Data](../../../kyberswap-solutions/kyberai/user-guides/deep-dive-into-token-data.md)
{% endtab %}
{% endtabs %}
