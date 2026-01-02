# Supported Exchanges And Networks

Chains and DEXs

The KyberSwap product suite has been deployed across the majority of the most established DeFi chains. Whichever your preferred network, you can secure the best rates via the [Aggregator](../kyberswap-solutions/kyberswap-aggregator/) (17 Chains, 400+ DEXs), execute precise trades with [Limit Orders](../kyberswap-solutions/limit-order/), or move assets seamlessly between networks using [Cross-chain Swaps](../kyberswap-solutions/kyberswap-interface/user-guides/cross-chain-swap.md). You can also utilize [KyberSwap Zap as a Service](../kyberswap-solutions/kyberswap-zap-as-a-service/) to effortlessly add liquidity into any concentrated liquidity protocol using any tokens, while also minimizing price impact through integration with the KyberSwap aggregator.

{% hint style="info" %}
**DEX filtering**

For traders, you can specify which DEXs are considered when computing your swap route by Customizing Trade Parameters directly on the [KyberSwap Interface](../kyberswap-solutions/kyberswap-interface/).

For developers integrating with the [KyberSwap Aggregator](../kyberswap-solutions/kyberswap-aggregator/), please refer to [DEX IDs](../kyberswap-solutions/kyberswap-aggregator/dex-ids.md) for internal mapping of DEXs used for filtering via the [API](../kyberswap-solutions/kyberswap-aggregator/aggregator-api-specification/).
{% endhint %}

| **Type** | **Network (Chain ID)** | **Aggregator** | **Limit Order** | **Zap** | **Cross-chain Swap** |
| -------- | ---------------------- | -------------- | --------------- | ------- | -------------------- |
| EVM      | Ethereum (1)           | ✅              | ✅               | ✅       | ✅                    |
| EVM      | BNB Chain (56)         | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Avalanche (43114)      | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Berachain (80094)      | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Sonic (146)            | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Ronin (2020)           | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Base (8453)            | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Arbitrum (42161)       | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Optimism (10)          | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Polygon POS (137)      | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Unichain               | ✅              | ✅               |         | ✅                    |
| EVM      | Linea (59144)          | ✅              | ✅               | ✅       | ✅                    |
| EVM      | HyperEVM (999)         | ✅              | ✅               |         | ✅                    |
| EVM      | Mantle (5000)          | ✅              | ✅               |         | ✅                    |
| EVM      | Plasma (9745)          | ✅              |                 |         | ✅                    |
| EVM      | Etherlink (42793)      | ✅              |                 |         | ✅                    |
| EVM      | zkSync                 |                |                 |         | ✅                    |
| EVM      | Scroll                 |                |                 |         | ✅                    |
| EVM      | Fantom                 |                |                 |         | ✅                    |
| EVM      | Blast                  |                |                 |         | ✅                    |
| Non-EVM  | NEAR                   |                |                 |         | ✅                    |
| Non-EVM  | Bitcoin                |                |                 |         | ✅                    |
| Non-EVM  | Solana                 |                |                 |         | ✅                    |

#### KyberEarn

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th width="169.6319580078125"></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Network</strong></td><td><strong>Uni V4 FF</strong></td><td><strong>Uni V4</strong></td><td><strong>Uni V3</strong></td><td><strong>Uni V2</strong></td><td><strong>Pancake ∞ CL FF</strong></td><td><strong>Pancake ∞ CL</strong></td><td><strong>Pancake ∞ CL Alpha</strong></td><td><strong>Pancake ∞ CL Brevis</strong></td><td><strong>Pancake ∞ CL Dynamic</strong></td><td><strong>Pancake ∞ CL LO</strong></td><td><strong>Pancake V3</strong></td><td><strong>Aerodrome Concentrated</strong></td><td><strong>Sushi V3</strong></td><td><strong>THENA</strong></td><td><strong>Camelot V3</strong></td><td><strong>QuickSwap V3</strong></td><td><strong>Kodiak</strong></td></tr><tr><td>Ethereum (1)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td></td><td>✅</td><td></td><td></td><td></td><td></td></tr><tr><td>Base (8453)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td></tr><tr><td>BNB Chain (56)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td>✅</td><td></td><td></td><td></td></tr><tr><td>Arbitrum (42161)</td><td></td><td></td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td></td><td>✅</td><td></td><td>✅</td><td></td><td></td></tr><tr><td>Optimism (10)</td><td></td><td></td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>Polygon POS (137)</td><td></td><td></td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td></td><td></td><td>✅</td><td></td></tr><tr><td>Avalanche (43114)</td><td></td><td></td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>Berachain (80094)</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td></tr></tbody></table>

<table data-view="cards"><thead><tr><th></th></tr></thead><tbody><tr><td><a data-mention href="/broken/pages/jGSQwkNNFqLTnHbPExjE">Broken link</a></td></tr><tr><td><a data-mention href="../kyberswap-solutions/kyberswap-zap-as-a-service/zaps-supported-chains-dexes.md">zaps-supported-chains-dexes.md</a></td></tr></tbody></table>
