# Supported Exchanges And Networks

The KyberSwap product suite has been deployed across the majority of the most established DeFi chains. Whichever your preferred network, you can secure the best rates via the [Aggregator](../kyberswap-solutions/kyberswap-aggregator/) (18 Chains, 420+ DEXs), execute precise trades with [Limit Orders](../kyberswap-solutions/limit-order/), or move assets seamlessly between networks using [Cross-chain Swaps](../user-guide/cross-chain-swap.md). You can also utilize [KyberSwap Zap as a Service](../kyberswap-solutions/kyberswap-zap-as-a-service/) to effortlessly add liquidity into any concentrated liquidity protocol using any tokens, while also minimizing price impact through integration with the KyberSwap aggregator.

{% hint style="info" %}
**DEX filtering**

For traders, you can specify which DEXs are considered when computing your swap route by Customizing Trade Parameters directly on the [KyberSwap Interface](../kyberswap-solutions/kyberswap-interface/).

For developers integrating with the [KyberSwap Aggregator](../kyberswap-solutions/kyberswap-aggregator/), please refer to [DEX IDs](../developer-guide/aggregator-api/dex-ids.md) for internal mapping of DEXs used for filtering via the [API](../developer-guide/aggregator-api/aggregator-api-specification/).
{% endhint %}

| **Type** | **Network (Chain ID)**                                       | **Aggregator** | **Limit Order** | **Zap** | **Cross-chain Swap** |
| -------- | ------------------------------------------------------------ | -------------- | --------------- | ------- | -------------------- |
| EVM      | Ethereum (1)                                                 | ✅              | ✅               | ✅       | ✅                    |
| EVM      | BNB Chain (56)                                               | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Avalanche (43114)                                            | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Berachain (80094)                                            | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Sonic (146)                                                  | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Ronin (2020)                                                 | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Base (8453)                                                  | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Arbitrum (42161)                                             | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Optimism (10)                                                | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Polygon POS (137)                                            | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Unichain (130)                                               | ✅              | ✅               |         | ✅                    |
| EVM      | Linea (59144)                                                | ✅              | ✅               | ✅       | ✅                    |
| EVM      | HyperEVM (999)                                               | ✅              | ✅               |         | ✅                    |
| EVM      | Plasma (9745)                                                | ✅              |                 |         | ✅                    |
| EVM      | Etherlink (42793)                                            | ✅              |                 |         | ✅                    |
| EVM      | MegaETH (4326)                                               | ✅              | ✅               |         | ✅                    |
| EVM      | Monad (143)                                                  | ✅              | ✅               | ✅       | ✅                    |
| EVM      | zkSync                                                       |                |                 |         | ✅                    |
| EVM      | Mantle (5000)                                                |                |                 |         | ✅                    |
| EVM      | Robinhood (4663)                                             | ✅              | ✅               | ✅       | ✅                    |
| EVM      | Rise (4153) <mark style="color:orange;">`Provisional`</mark> | ✅              | ✅               |         |                      |
| EVM      | Scroll                                                       |                |                 |         | ✅                    |
| EVM      | Fantom                                                       |                |                 |         | ✅                    |
| EVM      | Blast                                                        |                |                 |         | ✅                    |
| Non-EVM  | NEAR                                                         |                |                 |         | ✅                    |
| Non-EVM  | Bitcoin                                                      |                |                 |         | ✅                    |
| Non-EVM  | Solana                                                       |                |                 |         | ✅                    |

**Provisional networks** (with tag <mark style="color:orange;">`Provisional`</mark>) are newly added chains that are currently in an initial observation period. We keep these networks under close monitoring to evaluate their overall stability within the KyberSwap ecosystem. These networks provide the full KyberSwap experience with all supported functions available. However, please be aware that support for any provisional network may be discontinued following this evaluation.

#### Kyber Earn

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th width="169.6319580078125"></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Network</strong></td><td><strong>Uni V4 FF</strong></td><td><strong>Uni V4</strong></td><td><strong>Uni V3</strong></td><td><strong>Uni V2</strong></td><td><strong>Pancake ∞ CL FF</strong></td><td><strong>Pancake ∞ CL</strong></td><td><strong>Pancake ∞ CL Alpha</strong></td><td><strong>Pancake ∞ CL Brevis</strong></td><td><strong>Pancake ∞ CL Dynamic</strong></td><td><strong>Pancake ∞ CL LO</strong></td><td><strong>Pancake V3</strong></td><td><strong>Aerodrome Concentrated</strong></td><td><strong>Sushi V3</strong></td><td><strong>THENA</strong></td><td><strong>Camelot V3</strong></td><td><strong>QuickSwap V3</strong></td><td><strong>Kodiak</strong></td></tr><tr><td>Ethereum (1)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td></td><td>✅</td><td></td><td></td><td></td><td></td></tr><tr><td>Base (8453)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td></tr><tr><td>BNB Chain (56)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td>✅</td><td></td><td></td><td></td></tr><tr><td>Arbitrum (42161)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td></td><td>✅</td><td></td><td>✅</td><td></td><td></td></tr><tr><td>Optimism (10)</td><td></td><td></td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>Polygon POS (137)</td><td></td><td></td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td></td><td></td><td>✅</td><td></td></tr><tr><td>Avalanche (43114)</td><td></td><td></td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>Berachain (80094)</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td></tr><tr><td>Monad (143)</td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>Robinhood (4663) </td><td>✅</td><td>✅</td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>✅</td><td></td><td></td><td></td><td></td><td></td><td></td></tr></tbody></table>

#### Smart Exit

<table data-search="false"><thead><tr><th width="169.5078125">Network</th><th width="115.05859375">Uni V4 FF</th><th width="111.703125">Uni V4</th><th width="107.47265625">Uni V3</th><th width="119.48046875">Pancake ∞ CL FF</th><th width="119.98046875">Pancake ∞ CL</th><th>Pancake V3</th><th>SushiSwap V3</th></tr></thead><tbody><tr><td>Ethereum (1)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Base (8453)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>BNB Chain (56)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Arbitrum (42161)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Optimism (10)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Monad (143)</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Robinhood (4663) </td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td><td>✅</td></tr></tbody></table>
