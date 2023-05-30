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
   * [Instantly Swap At The Best Rates ](instantly-swap-at-the-best-rates.md)
   * **Swap At Your Preferred Rates <-**

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
