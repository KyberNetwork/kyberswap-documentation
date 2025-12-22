# Fee Schedule

1. **Introduction**\
   By using the Sites or the Services, a Transaction Fee may be charged for each transaction executed, for the use of or execution of transactions on a blockchain network or in connection with the Services. Therefore, in addition to the network fees associated with their transactions, KyberSwap may charge a Trading Fee depending on the product being used. This Trading Fee helps sustain the protocol, reward liquidity providers, and support order execution on-chain. The Fee Schedule below provides details of the specific fee for each product on KyberSwap.
2.  **Fee Summary Table**<br>

    <table><thead><tr><th align="center">Product</th><th width="163" align="center">Fee Type</th><th align="center">Fee Rate</th><th align="center" valign="middle">Note</th></tr></thead><tbody><tr><td align="center">Swap</td><td align="center">No fee</td><td align="center">No fee</td><td align="center" valign="middle"></td></tr><tr><td align="center">Limit Order</td><td align="center">Fixed</td><td align="center">0.01% - 1%</td><td align="center" valign="middle">depends on volatility level of the tokens</td></tr><tr><td align="center">Earn</td><td align="center">Fixed</td><td align="center">0.01% - 0.25%</td><td align="center" valign="middle"></td></tr><tr><td align="center">Widget/ iFrame</td><td align="center">Variable</td><td align="center">Variable</td><td align="center" valign="middle">Configured by protocol using (not by KyberSwap)</td></tr><tr><td align="center">Cross-chain Swap</td><td align="center">Fixed</td><td align="center">0.05% - 0.25%</td><td align="center" valign="middle">depends on route and volatility level of the tokens</td></tr><tr><td align="center">Other value-added service (Market Overview, Analytics, Token Checker, and MEV Protection)</td><td align="center">No fee</td><td align="center">No fee</td><td align="center" valign="middle"></td></tr></tbody></table>

    <br>
3. **Product-Specific Fee Details**
   1.  **Swap**

       KyberSwap does not charge fees to users using the protocol to swap tokens. However Liquidity Providers are allowed to set fees on their liquidity pools and traders who choose to use these pools to perform swaps will need to pay trading fees to the LP, along with any associated network fees.
   2.  **Limit Order**

       To support the continued development of the Limit Orders feature, KyberSwap will charge variable taker fees for orders filled on the following chains:

       * Ethereum (ChainID: 1)
       * BSC (ChainID: 56)
       * Arbitrum (ChainID: 42161)
       * Polygon (ChainID: 137)
       * Optimism (ChainID: 10)
       * Avalanche (ChainID: 43114)
       * Fantom (ChainID: 250)
       * Base (ChainID: 8453)
       * ZkSync (ChainID: 324)
       * Linea (ChainID: 59144)
       * Mantle (ChainID: 5000)
       * Scroll (ChainID: 534352)
       * Blast (ChainID: 81457)

       The fees charged will be according to the most exotic token in the trading pair. The section below lists the fees whereby the highest fee category will apply based on the classification of the input and output tokens. There are 4 categories of tokens with an additional special category for trades involving KNC.

       **Super stable (0.01%)**

       * Ethereum (ChainID: 1)
         * USDC: [`0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`](https://etherscan.io/address/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48)
         * USDT: [`0xdac17f958d2ee523a2206206994597c13d831ec7`](https://etherscan.io/address/0xdac17f958d2ee523a2206206994597c13d831ec7)
         * DAI: [`0x6b175474e89094c44da98b954eedeac495271d0f`](https://etherscan.io/address/0x6b175474e89094c44da98b954eedeac495271d0f)
       * BSC (ChainID: 56)
         * USDT: [`0x55d398326f99059ff775485246999027b3197955`](https://bscscan.com/address/0x55d398326f99059ff775485246999027b3197955)
         * USDC: [`0x8ac76a51cc950d9822d68b83fe1ad97b32cd580d`](https://bscscan.com/address/0x8ac76a51cc950d9822d68b83fe1ad97b32cd580d)
         * DAI: [`0x1af3f329e8be154074d8769d1ffa4ee058b1dbc3`](https://bscscan.com/address/0x1af3f329e8be154074d8769d1ffa4ee058b1dbc3)
         * BUSD: [`0xe9e7cea3dedca5984780bafc599bd69add087d56`](https://bscscan.com/address/0xe9e7cea3dedca5984780bafc599bd69add087d56)
       * Arbitrum (ChainID: 42161)
         * USDT: [`0xFd086bC7CD5C481DCC9C85ebE478A1C0b69FCbb9`](https://arbiscan.io/address/0xFd086bC7CD5C481DCC9C85ebE478A1C0b69FCbb9)
         * USDC: [`0xaf88d065e77c8cC2239327C5EDb3A432268e5831`](https://arbiscan.io/address/0xaf88d065e77c8cC2239327C5EDb3A432268e5831)
         * DAI: [`0xDA10009cBd5D07dd0CeCc66161FC93D7c9000da1`](https://arbiscan.io/address/0xDA10009cBd5D07dd0CeCc66161FC93D7c9000da1)
       * Polygon (ChainID: 137)
         * USDT: [`0xc2132d05d31c914a87c6611c10748aeb04b58e8f`](https://polygonscan.com/address/0xc2132d05d31c914a87c6611c10748aeb04b58e8f)
         * USDC: [`0x2791bca1f2de4661ed88a30c99a7a9449aa84174`](https://polygonscan.com/address/0x2791bca1f2de4661ed88a30c99a7a9449aa84174)
         * DAI: [`0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063`](https://polygonscan.com/address/0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063)
       * Optimism (ChainID: 10)
         * USDT: [`0x94b008aa00579c1307b0ef2c499ad98a8ce58e58`](https://optimistic.etherscan.io/address/0x94b008aa00579c1307b0ef2c499ad98a8ce58e58)
         * USDC: [`0x7f5c764cbc14f9669b88837ca1490cca17c31607`](https://optimistic.etherscan.io/address/0x7f5c764cbc14f9669b88837ca1490cca17c31607)
         * DAI: [`0xda10009cbd5d07dd0cecc66161fc93d7c9000da1`](https://optimistic.etherscan.io/address/0xda10009cbd5d07dd0cecc66161fc93d7c9000da1)
       * Avalanche (ChainID: 43114)
         * USDT: [`0x9702230A8Ea53601f5cD2dc00fDBc13d4dF4A8c7`](https://snowtrace.io/address/0x9702230A8Ea53601f5cD2dc00fDBc13d4dF4A8c7)
         * USDC: [`0xB97EF9Ef8734C71904D8002F8b6Bc66Dd9c48a6E`](https://snowtrace.io/address/0xB97EF9Ef8734C71904D8002F8b6Bc66Dd9c48a6E)
         * DAI.e: [`0xd586E7F844cEa2F87f50152665BCbc2C279D8d70`](https://snowtrace.io/address/0xd586E7F844cEa2F87f50152665BCbc2C279D8d70)
         * USDT.e: [`0xc7198437980c041c805A1EDcbA50c1Ce5db95118`](https://snowtrace.io/address/0xc7198437980c041c805A1EDcbA50c1Ce5db95118)
         * USDC.e: [`0xA7D7079b0FEaD91F3e65f86E8915Cb59c1a4C664`](https://snowtrace.io/address/0xA7D7079b0FEaD91F3e65f86E8915Cb59c1a4C664)
       * Fantom (ChainID: 250)
         * fUSDT: [`0x049d68029688eabf473097a2fc38ef61633a3c7a`](https://ftmscan.com/address/0x049d68029688eabf473097a2fc38ef61633a3c7a)
         * USDC: [`0x04068DA6C83AFCFA0e13ba15A6696662335D5B75`](https://ftmscan.com/address/0x04068DA6C83AFCFA0e13ba15A6696662335D5B75)
         * DAI: [`0x8D11eC38a3EB5E956B052f67Da8Bdc9bef8Abf3E`](https://ftmscan.com/address/0x8D11eC38a3EB5E956B052f67Da8Bdc9bef8Abf3E)

       **Stable (0.02%)**

       * Ethereum (ChainID: 1)
         * MAI: [`0x8D6CeBD76f18E1558D4DB88138e2DeFB3909fAD6`](https://etherscan.io/address/0x8D6CeBD76f18E1558D4DB88138e2DeFB3909fAD6)
         * BOB: [`0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B`](https://etherscan.io/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
         * MIM: [`0x99D8a9C45b2ecA8864373A26D1459e3Dff1e17F3`](https://etherscan.io/address/0x99D8a9C45b2ecA8864373A26D1459e3Dff1e17F3)
       * BSC (ChainID: 56)
         * MAI: [`0x3F56e0c36d275367b8C502090EDF38289b3dEa0d`](https://bscscan.com/address/0x3F56e0c36d275367b8C502090EDF38289b3dEa0d)
         * BOB: [`0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B`](https://bscscan.com/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
         * MIM: [`0xfE19F0B51438fd612f6FD59C1dbB3eA319f433Ba`](https://bscscan.com/address/0xfE19F0B51438fd612f6FD59C1dbB3eA319f433Ba)
       * Arbitrum (ChainID: 42161)
         * MAI: [`0x3F56e0c36d275367b8C502090EDF38289b3dEa0d`](https://arbiscan.io/address/0x3F56e0c36d275367b8C502090EDF38289b3dEa0d)
         * MIM: [`0xFEa7a6a0B346362BF88A9e4A88416B77a57D6c2A`](https://arbiscan.io/address/0xFEa7a6a0B346362BF88A9e4A88416B77a57D6c2A)
       * Polygon (ChainID: 137)
         * MAI: [`0xa3Fa99A148fA48D14Ed51d610c367C61876997F1`](https://polygonscan.com/address/0xa3Fa99A148fA48D14Ed51d610c367C61876997F1)
         * BOB: [`0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B`](https://polygonscan.com/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
         * MIM: [`0x49a0400587A7F65072c87c4910449fDcC5c47242`](https://polygonscan.com/address/0x49a0400587A7F65072c87c4910449fDcC5c47242)
       * Optimism (ChainID: 10)
         * MAI: [`0xdFA46478F9e5EA86d57387849598dbFB2e964b02`](https://optimistic.etherscan.io/address/0xdFA46478F9e5EA86d57387849598dbFB2e964b02)
         * BOB: [`0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B`](https://optimistic.etherscan.io/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
       * Avalanche (ChainID: 43114)
         * MAI: [`0x5c49b268c9841AFF1Cc3B0a418ff5c3442eE3F3b`](https://snowtrace.io/address/0x5c49b268c9841AFF1Cc3B0a418ff5c3442eE3F3b)
         * YUSD: [`0x111111111111ed1D73f860F57b2798b683f2d325`](https://snowtrace.io/address/0x111111111111ed1D73f860F57b2798b683f2d325)
         * MIM: [`0x130966628846BFd36ff31a822705796e8cb8C18D`](https://snowtrace.io/address/0x130966628846BFd36ff31a822705796e8cb8C18D)
       * Fantom (ChainID: 250)
         * MAI: [`0xfB98B335551a418cD0737375a2ea0ded62Ea213b`](https://ftmscan.com/address/0xfB98B335551a418cD0737375a2ea0ded62Ea213b)
         * MIM: [`0x82f0B8B456c1A451378467398982d4834b6829c1`](https://ftmscan.com/address/0x82f0B8B456c1A451378467398982d4834b6829c1)

       **Normal (0.1%)**

       * Top 200 tokens by market cap (identified via multiple on and off-chain services), excluding tokens under the super stable, stable, and KNC categories.

       **Exotic (0.3%)**

       * All remaining tokens not covered in the super stable, stable, normal, and KNC categories.

       **High Volatility (0.5%)**

       * Tokens that have been added in the Token Catalog from 2 weeks to 1 month.

       **Super High Volatility (1%)**

       * Tokens that have been added in the Token Catalog for less than 2 weeks.

       **KNC (0.1%)**

       * Trades to and from KNC will be charged a flat 0.1% fee.
   3.  **Earn**

       There are two types of fees incorporated into the Zap API:\
       \
       **Protocol fees**

       Protocol fees are charged by KyberSwap in input token for Zap. In feature, and are based on 4 different token pair categories:

       | Pair Category   | Protocol Fee |
       | --------------- | ------------ |
       | Stable pair     | 0.01%        |
       | Correlated pair | 0.025%       |
       | Common pair     | 0.1%         |
       | Exotic pair     | 0.25%        |

       * Please refer to the example file below for a list of PancakeSwap v3 pools for each of the category above. PancakeSwap v3 pools not in the list belongs to the "Exotic pair" category.<br>

       **Partner fees**

       * Partner fee configuration is sent by the partner client via the API to charge a partner fee on top of the protocol fees
       * Similar to protocol fees, partners will only be able to charge the fee by the input token for Zap In.
       * Provides both a valid non-zero feeAddress and a positive integer feePcm (the unit is per cent mille, i.e. 1-1000th of 1%) in the API call to [GetRoute](kyberswap-zap-as-a-service/kyberswap-zap-as-a-service-zaas-api/zaas-http-api.md#get-route). Otherwise, no fee will be collected for partner.
   4.  **Widget/ iFrame**\
       The Widget/iFrame fee structure is **not applied universally across all integrations**; it depends on the specific protocols using it. These fees are not technically charged by KyberSwap—instead, they are configured by the partner protocols themselves. KyberSwap provides the underlying infrastructure that enables these protocols to implement and manage their custom fee customizations.

       Users trading directly on [KyberSwap.com](http://kyberswap.com/) UI are not subject to this fee structure.
   5.  **Cross-chain Swap**

       To support the continued development and maintenance of the Cross-Chain Swap, KyberSwap applies a platform fee for using this feature. Below is the detailed fee structure:

       <table data-header-hidden><thead><tr><th></th><th width="181.61328125"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Route</strong></td><td><strong>Stable tokens &#x26; Same native token</strong></td><td><strong>Common</strong></td><td><strong>Exotic</strong></td><td><strong>High-volatility</strong></td></tr><tr><td><strong>EVM ↔ EVM</strong></td><td>0.05 %</td><td>0.10 %</td><td>0.15 %</td><td>0.25 %</td></tr><tr><td><strong>Near ↔ EVM</strong></td><td>0.1%</td><td>0.2%</td><td>0.2%</td><td>0.2%</td></tr><tr><td><strong>Solana ↔ EVM</strong></td><td>0.1%</td><td>0.2%</td><td>0.2%</td><td>0.2%</td></tr><tr><td><strong>BTC ↔ EVM</strong></td><td>0.25 % </td><td>0.25 % </td><td>0.25 % </td><td>0.25 % </td></tr><tr><td><strong>Non-EVM ↔ Non-EVM</strong></td><td>0.25 %</td><td>0.25 % </td><td>0.25 % </td><td>0.25 %</td></tr></tbody></table>



_Additional notes:_

_\*For Third Party Integrated Services, users are responsible for complying with the third party's fee schedule._

_\*\*This Fee Schedule may be updated from time to time by KyberSwap. Please refer to our Terms of Use for further details._\
<br>
