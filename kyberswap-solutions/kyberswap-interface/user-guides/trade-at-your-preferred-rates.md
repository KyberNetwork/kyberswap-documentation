---
description: Trade On Your Own Terms
---

# Swap At Your Preferred Rates

## Introduction to Limit Orders on KyberSwap

A [**Limit Order** ](../../limit-order/)is a way for KyberSwap traders to swap tokens at a specified price or better. This stipulation allows you to have better control over your prices and capital efficiency. Limit orders are not sent to any specific user, but can instead be filled by anyone, including the KyberSwap aggregator. You can also create limit orders via KyberSwap APIs. When the market price matches the price set in the limit order, a **taker** can fill it. When a taker fills the order, the taker pays the gas fees associated with the transaction

<details>

<summary>Trader Flow</summary>

1. [Connect Your Wallet ](connect-your-wallet.md)
2. [Switching Networks ](selecting-preferred-network.md)
3. Get Tokens
   * [Get Crypto With Fiat](get-crypto-with-fiat.md)
   * [Bridge Your Assets Across Multiple Chains](bridge-your-assets-across-multiple-chains.md)
4. Swap Tokens
   * [Instantly Swap At Superior Rates ](broken-reference)
   * **Swap At Your Preferred Rates <-**
   * [Swap Between Different Tokens Across Chains](swap-between-different-tokens-across-chains.md)

</details>

## How to create a limit order

<details>

<summary>Limit Order protocol fees</summary>

To support the continued development of the Limit Orders feature, KyberSwap will charge variable maker fees for orders filled on the following chains:

* BSC (ChainID: 56)
* Fantom (ChainID: 250)
* Polygon (ChainID: 137)
* Optimism (ChainID: 10)
* Avalanche (ChainID: 43114)

The fees charged will be according to the most exotic token in the trading pair. The section below lists the fees whereby the highest fee category will apply based on the classification of the tokens involved. There are 4 categories of tokens with an additional special category for trades involving KNC.

**Super stable (0.01%)**

* BSC (ChainID: 56)
  * USDT: [`0x55d398326f99059ff775485246999027b3197955`](https://bscscan.com/address/0x55d398326f99059ff775485246999027b3197955)
  * USDC: [`0x8ac76a51cc950d9822d68b83fe1ad97b32cd580d`](https://bscscan.com/address/0x8ac76a51cc950d9822d68b83fe1ad97b32cd580d)
  * DAI: [`0x1af3f329e8be154074d8769d1ffa4ee058b1dbc3`](https://bscscan.com/address/0x1af3f329e8be154074d8769d1ffa4ee058b1dbc3)&#x20;
  * BUSD: [`0xe9e7cea3dedca5984780bafc599bd69add087d56`](https://bscscan.com/address/0xe9e7cea3dedca5984780bafc599bd69add087d56)
* Fantom (ChainID: 250)
  * fUSDT: [`0x049d68029688eabf473097a2fc38ef61633a3c7a`](https://ftmscan.com/address/0x049d68029688eabf473097a2fc38ef61633a3c7a)
  * USDC: [`0x04068DA6C83AFCFA0e13ba15A6696662335D5B75`](https://ftmscan.com/address/0x04068DA6C83AFCFA0e13ba15A6696662335D5B75)
  * DAI: [`0x8D11eC38a3EB5E956B052f67Da8Bdc9bef8Abf3E`](https://ftmscan.com/address/0x8D11eC38a3EB5E956B052f67Da8Bdc9bef8Abf3E)
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

**Stable (0.02%)**

* BSC (ChainID: 56)
  * MAI: [`0x3F56e0c36d275367b8C502090EDF38289b3dEa0d`](https://bscscan.com/address/0x3F56e0c36d275367b8C502090EDF38289b3dEa0d)
  * BOB: [`0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B`](https://bscscan.com/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
  * MIM: [`0xfE19F0B51438fd612f6FD59C1dbB3eA319f433Ba`](https://bscscan.com/address/0xfE19F0B51438fd612f6FD59C1dbB3eA319f433Ba)
* Fantom (ChainID: 250)
  * MAI: [`0xfB98B335551a418cD0737375a2ea0ded62Ea213b`](https://ftmscan.com/address/0xfB98B335551a418cD0737375a2ea0ded62Ea213b)
  * MIM: [`0x82f0B8B456c1A451378467398982d4834b6829c1`](https://ftmscan.com/address/0x82f0B8B456c1A451378467398982d4834b6829c1)
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

**Normal (0.1%)**

* Top 200 tokens by market cap (identified via multiple on and off-chain services), excluding tokens under the super stable, stable, and KNC categories.

**Exotic (0.3%)**

* All remaining tokens not covered in the super stable, stable, normal, and KNC categories.

**KNC (0.05%)**

* Trades to and from KNC will be charged a flat 0.05% fee.

</details>

### **Step 1: Connect your wallet**

[Connect your Web3 wallet to KyberSwap](https://support.kyberswap.com/hc/en-us/articles/13757914421273) and select the network that you would like to use for the swap using the selector at the top right of the Swap page.

![Select network](https://support.kyberswap.com/hc/article\_attachments/14668135326105)

### **Step 2**: Navigate to the limit order page

From the Swap page, click the “Limit” tab on the token swap interface. This brings up the limit order interface.

![Limit order screen](https://support.kyberswap.com/hc/article\_attachments/14668135361561)

### **Step 3**: Specify your swap pair

You can either do this manually using the individual token selection buttons on the swap screen or by searching for your desired swap pair using the search field. (The keyboard shortcut Ctrl+K also opens this search feature.)

![USDC-KNC search](https://support.kyberswap.com/hc/article\_attachments/14668185799449)

{% hint style="warning" %}
#### Fee-on-transfer tokens

Note that certain ERC20 token smart contracts implement a fee-on-transfer (FOT) mechanism whereby for every token transfer, a percentage of the tokens are burned or distributed to various wallets. As a permissionless dapp, KyberSwap enables users to [Add Their Favourite Tokens](add-your-favourite-tokens.md) and hence do not limit the type of tokens traded as long as the token follows the [ERC20 standard](https://docs.openzeppelin.com/contracts/4.x/erc20).

Specific to limit orders, tokens are transferred after a maker order has been matched with a taker order (not including FOT tax). As such, the party that incurs the FOT tax will be dependent on the direction of the swap:

* **Output token**: In the case whereby a standard token is being traded for a FOT token, the FOT token is being transferred from the maker to the taker. Maker will receive the standard token less the swap fees while taker will receive the FOT token minus the swap fees AND FOT tax.
* **Input token**: In the case whereby a FOT token is being traded for a standard token, the FOT token is being transferred from the taker to the maker. Maker will receive the FOT token less the swap fees AND fee-on-transfer while taker will receive the standard token minus the swap fees.

For a swap between two FOT tokens, the FOT tax will be incurred by both parties. If the limit order is filled via the [KyberSwap Aggregator](../../kyberswap-aggregator/), there will be an additional token hop via the aggregator smart contract hence the FOT tax will also be charged on the additional hop.

Note that the FOT tax is specified in the FOT token's smart contract (i.e. the FOT token team) hence KyberSwap does not have any control over the FOT mechanism. Users are advised to trade such tokens at their own risk as KyberSwap was optimized to handle the standard ERC20 implementation.
{% endhint %}

### **Step 4**: Configure your order amount

Specify the amount you would like to offer by typing in an amount manually into the “You Pay” field. Please ensure that your wallet balance is sufficient to cover the swap offer.

![Specify offer amount.png](https://support.kyberswap.com/hc/article\_attachments/14668185864985)

### **Step 5**: Configure your order price

Set the price by manually entering a price at the “Sell \[token] at rate”. This will calculate an estimate of the amount you should receive in the “You Receive” field. KyberSwap will provide you with a percentage estimate of how much more favorable/unfavorable to you (the market maker) the specified price is relative to the current market price.

![Specify price](https://support.kyberswap.com/hc/article\_attachments/14668151102489)

### **Step 6**: Specify the time limit of your order

If your order is not filled by the end of this time limit, it will be automatically cancelled. You can either select from a list of set times or specify a custom expiry time and date. Note that you can still manually cancel your order (or any unfilled portion of your order) before it expires.

![Set expiry for order](https://support.kyberswap.com/hc/article\_attachments/14668186069529)

### **Step 7**: Approve contract to spend tokens

If this is the first time you are swapping this token on this network, click on “Approve \[Token]”. Your wallet will prompt you to give your approval (an onchain transaction requiring gas) for the KyberSwap smart contract to transact using this token on this network. This is a one-time action and subsequent swaps involving this token will not require further approvals unless there is an update to the smart contract.

{% hint style="info" %}
#### Asset balances and token allowance

By setting a token allowance, you are allowing the KyberSwap contract to transfer the the available amount of tokens in your wallet. Your tokens will remain in your wallet until the limit order is executed. However, in cases whereby your wallet contains insufficient tokens for the limit order to be completed (i.e. tokens are removed from wallet or tokens were used for earlier orders), your outstanding limit order will not be filled. The limit order token amount is capped by the available tokens in your wallet at the point of order creation.
{% endhint %}

![Approve USDC](https://support.kyberswap.com/hc/article\_attachments/14668151296537)

### **Step 8**: Review and confirm your order

Click on “Review Order” to bring up the preview screen. Once you are satisfied with the details of the limit order, click “Place Order” to proceed.

![Review limit order](https://support.kyberswap.com/hc/article\_attachments/14668186328089)

You will need to confirm this onchain transaction in your web3 wallet.

![Transaction pending confirmation](https://support.kyberswap.com/hc/article\_attachments/14668151529369)

Once the order has been confirmed you should see it appear in the Active Orders screen of the swap interface.

![Active orders](https://support.kyberswap.com/hc/article\_attachments/14668186560537)

Note: When your order is _completely_ filled it will be moved to the Order History tab of this interface.

{% hint style="info" %}
#### Limit order and wallet balances

Tokens which have been comitted to the limit order will only be deducted from the maker's wallet when a matching taker order is settled on-chain. This means that, up until the point when the limit order is executed the tokens remain available in your wallet and can be used in any of the usual ways. During execution, if there are insufficient tokens in your wallet, the limit order will not fill and therefore result in a failed transaction.

Limit orders can only be created if the user has sufficient token balances in their wallet at the point of placing the maker order.
{% endhint %}
