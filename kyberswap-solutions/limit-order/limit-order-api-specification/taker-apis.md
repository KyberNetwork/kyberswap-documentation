---
description: KyberSwap Limit Order Taker APIs
---

# Taker APIs

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" %}

## Taker APIs

<details>

<summary>API statuses and support</summary>

KyberSwap APIs uses the following statuses to minimize version miscommunications and ensure an uninterrupted service for the end user:

* `Latest`: API is functional and supported. This is the recommended version for all integrators (new and existing).
* `Legacy`: API remains functional with support for bugs only. No new feature updates.
* `Deprecated`: API is no longer functional and is not supported.

For all developers, it is highly recommended that you refer to the API with the `Latest` tag to ensure access to the latest features as well as improved service quality and efficiency. APIs which are planned to be sunset will be tagged `Legacy` during the transition period and thereafter moved to `Deprecated`.

The KyberSwap Docs will continue to maintain information regarding `Legacy` and `Deprecated` APIs.

</details>

<details>

<summary>Limit Order protocol fees</summary>

To support the continued development of the Limit Orders feature, KyberSwap will charge variable taker fees for orders filled on the following chains:

* Ethereum (ChainID: 1)
* BSC (ChainID: 56)
* Arbitrum (ChainID: 42161)
* Polygon (ChainID: 137)
* Optimism (ChainID: 10)
* Avalanche (ChainID: 43114)
* Fantom (ChainID: 250)

The fees charged will be according to the most exotic token in the trading pair. The section below lists the fees whereby the highest fee category will apply based on the classification of the input and output tokens. There are 4 categories of tokens with an additional special category for trades involving KNC.

**Super stable (0.01%)**

* Ethereum (ChainID: 1)
  * USDC: [`0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`](https://etherscan.io/address/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48)
  * USDT: [`0xdac17f958d2ee523a2206206994597c13d831ec7`](https://etherscan.io/address/0xdac17f958d2ee523a2206206994597c13d831ec7)
  * DAI: [`0x6b175474e89094c44da98b954eedeac495271d0f`](https://etherscan.io/address/0x6b175474e89094c44da98b954eedeac495271d0f)
* BSC (ChainID: 56)
  * USDC: [`0x8ac76a51cc950d9822d68b83fe1ad97b32cd580d`](https://bscscan.com/address/0x8ac76a51cc950d9822d68b83fe1ad97b32cd580d)
  * USDT: [`0x55d398326f99059ff775485246999027b3197955`](https://bscscan.com/address/0x55d398326f99059ff775485246999027b3197955)
  * DAI: [`0x1af3f329e8be154074d8769d1ffa4ee058b1dbc3`](https://bscscan.com/address/0x1af3f329e8be154074d8769d1ffa4ee058b1dbc3)&#x20;
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

**KNC (0.05%)**

* Trades to and from KNC will be charged a flat 0.05% fee.

</details>

<details>

<summary>Rates calculation</summary>

$$rate =\frac{(\text{makingAmount}-\text{makingAmountFilled})*(1-\text{makerTokenFee%})*(\text{makerAssetPriceUSD}-\text{gasPriceUSD})}{(\text{takingAmount}-\text{takingAmountFilled})*\text{takerAssetPriceUSD}}$$

</details>

### `Latest`

{% hint style="success" %}
**Developer Guide**

Please refer to [**Fill Limit Order**](../developer-guides/fill-limit-order.md) for the relevant sequence diagram as well as a TypeScript example.
{% endhint %}

#### Query Order(s)

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-partner/api/v1/orders" method="get" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

#### Get Operator Signature

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-partner/api/v1/orders/operator-signature" method="get" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

#### Fill Order(s)

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-ks/api/v1/encode/fill-order-to" method="post" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-ks/api/v1/encode/fill-batch-orders-to" method="post" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}
