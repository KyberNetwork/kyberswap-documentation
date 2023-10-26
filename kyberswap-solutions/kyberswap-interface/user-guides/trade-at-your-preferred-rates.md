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
   * [Bridge Your Tokens](bridge-your-assets-across-multiple-chains.md)
4. Swap Tokens
   * [Instantly Swap At Superior Rates ](instantly-swap-at-superior-rates.md)
   * **Swap At Your Preferred Rates <-**
   * [Swap Between Different Tokens Across Chains](swap-between-different-tokens-across-chains.md)

</details>

## How to create a limit order

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

{% hint style="info" %}
#### Taker gas fees and filling of orders

KyberSwap LO uses an [off-chain relay, on-chain settlement](../../limit-order/concepts/off-chain-relay.md) mechanism which enables makers to create orders without requiring gas fees to be paid. However, takers of an order will have to incur a gas fee to settle the order on-chain. Depending on the chain where the LO is taking place, these gas fees could result in smaller trades being unprofitable.

For example, if it costs a taker 40USD in gas fees to settle an Ethereum LO on-chain, takers will unlikely execute smaller volume trades due to the transaction costs. As such, maker LOs with lower volumes will likely not be filled unless the price diverges significantly enough to justify a taker's gas fees. This effect is less pronounced on other chains where gas fees tend to be negligible.

To increase the likelihood that your LO will be filled, KyberSwap UI provides a handy helper whenever it detects that the current LO volume would likely result in unfilled orders.

![](../../../.gitbook/assets/LO\_UserGuide\_TakerGasFeesFillRate.png)
{% endhint %}

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

Once the order has been confirmed you should see it appear in the Active Orders screen of the swap interface. You can select individual orders to view the price history for the order pair.

![Active orders](https://support.kyberswap.com/hc/article\_attachments/14668186560537)

Note: When your order is _completely_ filled it will be moved to the Order History tab of this interface.

{% hint style="info" %}
#### Limit order and wallet balances

Tokens which have been comitted to the limit order will only be deducted from the maker's wallet when a matching taker order is settled on-chain. This means that, up until the point when the limit order is executed the tokens remain available in your wallet and can be used in any of the usual ways. During execution, if there are insufficient tokens in your wallet, the limit order will not fill and therefore result in a failed transaction.

Limit orders can only be created if the user has sufficient token balances in their wallet at the point of placing the maker order.
{% endhint %}
