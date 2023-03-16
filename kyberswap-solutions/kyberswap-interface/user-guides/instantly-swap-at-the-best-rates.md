---
description: Sourcing The Most Capitally Efficient Liquidity For Your Trade
---

# Instantly Swap At The Best Rates

## Introduction

KyberSwap allows you to swap tokens easily at the best rates by aggregating liquidity from different DEXs on the network. Through splitting and optimizing trade routes across various liquidity sources, KyberSwap is able to source the best rates for your swap.

Please refer to [Supported Exchanges and Networks](../../../getting-started/supported-exchanges-and-networks.md) for the full list of decentralized exchanges which have been integrated with KyberSwap.

<details>

<summary>Trader Flow</summary>

1. [Connect Your Wallet ](connect-your-wallet.md)
2. [Switching Networks ](selecting-preferred-network.md)****
3. Get Tokens
   * [Get Crypto With Fiat](get-crypto-with-fiat.md)
   * [Bridge Your Assets Across Multiple Chains](bridge-your-assets-across-multiple-chains.md)
4. Swap Tokens
   * **Instantly Swap At The Best Rates** **<-**
   * [Swap At Your Preferred Rates](trade-at-your-preferred-rates.md)

</details>

## Find the best rates for your swaps

### **Step 1: Connect your wallet**

[Connect your Web3 wallet to KyberSwap](connect-your-wallet.md) and [select the network](selecting-preferred-network.md) that you would like to use for the swap using the selector at the top right of the Swap page.

![Connected chain and wallet](https://support.kyberswap.com/hc/article\_attachments/13999999636249)

### **Step 2:** Specify your swap pair

&#x20;You can either do this manually using the individual token selection buttons on the swap screen

![Specify token individually](https://support.kyberswap.com/hc/article\_attachments/14746734857625)

or by searching for your desired swap pair using the search field. (The keyboard shortcut Ctrl+K also opens this search feature.)

![Swap via smart search](https://support.kyberswap.com/hc/article\_attachments/14746770685465)

### **Step 3**: Configure swap amount

Specify the amount you would like to swap by either typing in an amount manually or by using the “Max” and “Half” buttons to swap pre-set proportions of your wallet balance. An estimate of the amount returned should appear in the quote field.

KyberSwap Interface allows users to customize trade parameters which enables greater trade security or even more advanced trade strategies. Refer to [Customizing trade parameters](instantly-swap-at-the-best-rates.md#customizing-trade-parameters) section for more details.

{% hint style="info" %}
#### Route refresh: Ensuring the best rates

Do note that the KyberSwap Interface will continuously update the swap rates in order to source the best rates for your swap given the changing market conditions. As such, you will always be able to see the latest proposed route and rates prior to clicking the "Swap" button.

Upon clicking the "Swap" button, KyberSwap Aggregator will attempt to secure the final route that will be displayed on the "Confirm Swap" pop-up (see [Step 5](instantly-swap-at-the-best-rates.md#step-5-confirm-the-swap)).
{% endhint %}

![Specify swap amount](https://support.kyberswap.com/hc/article\_attachments/14746766951449)

{% hint style="info" %}
#### Slippage tolerance: Protecting your trades

KyberSwap allows you to avoid any negative trade outcomes by setting a [slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md) tolerance. Please refer to [Customizing trade parameters](instantly-swap-at-the-best-rates.md#customizing-trade-parameters) below for further details.
{% endhint %}

### **Step 4**: Approve or permit contract to swap tokens

Approve or Permit KyberSwap to swap the tokens on your behalf. Proceed to Step 5 if token approval/permit is not required.

If this is the first time you are swapping this token on this network using this wallet, the "Swap" button will be greyed out. You will first need to approve/permit the KyberSwap smart contract to spend your tokens before proceeding with the swap.

In the pursuit of greater gas savings for our users, KyberSwap has implemented a permit option for tokens which follow the [EIP-2612](https://eips.ethereum.org/EIPS/eip-2612) standard. In contrast to the basic [ERC20](../../../getting-started/foundational-topics/decentralized-finance/tokens.md#token-standards) token implementation, EIP-2612 enables gasless approvals of smart contract allowances with just a signed message. In other words, approving a token via "Permit" does not require any gas and achieves the same effect as the ERC20 "Approve". If you see a "Permit" button, it means your token is eligible for gasless approvals!

{% tabs %}
{% tab title="Permit" %}
Click on the "Permit \[Token]" button to allow KyberSwap to swap the tokens on your behalf.

<figure><img src="../../../.gitbook/assets/image (63).png" alt=""><figcaption><p>Permit EIP-2612 compatible tokens</p></figcaption></figure>

Upon clicking the "Permit" button, your wallet will prompt you to sign the transaction. Notice that no gas was required in this case!

{% hint style="info" %}
#### A note on permits

By permitting the swap, you are authorizing KyberSwap to swap the exact amount of tokens specified in the trade for the next 24 hours. This 24 hour deadline is implemented as a safety mechanism to ensure that the permit expires in case a corresponding swap order was not submitted or in the highly improbable event that an order was not filled. A new permit will be required upon the expiration of the current permit.&#x20;

Note that the granting of a permit and the confirmation of a swap ([step 5](instantly-swap-at-the-best-rates.md#step-5-confirm-the-swap)) are separate transactions whereby the latter is unable to proceed without the completion of the former. More importantly, as opposed to permits, swaps will always require gas to be paid as token transfers have to be confirmed by the network. As such, in the case whereby a swap remains in a pending state, it is possible to cancel the swap transaction in your wallet while the permit remains valid until expiry. If a future swap requires more tokens than an existing permit, the user will be requested to sign a new permit.
{% endhint %}
{% endtab %}

{% tab title="Approve" %}
Click on the "Approve \[Token]" button to allow KyberSwap to swap the tokens on your behalf.

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption><p>Approve ERC20 token</p></figcaption></figure>

To ensure the safety of your tokens, KyberSwap will also prompt you to select an allowance limit for the token being approved. By setting an allowance limit, this ensures that KyberSwap is only able to swap the specified number of tokens from your wallet. As long as the accumulated tokens for current or future swaps exceeds this limit, another approve process will be required. You can either set a custom allowance limit or opt for an infinite limit.

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption><p>Approve allowance popup</p></figcaption></figure>

Hovering your mouse above the options will also bring up the helpers for your convenience.

<figure><img src="../../../.gitbook/assets/image (85).png" alt=""><figcaption><p>Infinite allowance helper</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption><p>Custom allowance helper</p></figcaption></figure>

Upon confirming an allowance limit, your wallet will then prompt you to sign the transaction request with the relevant gas fees.
{% endtab %}
{% endtabs %}

### **Step 5**: Confirm the swap

Click the “Swap” button to bring up the confirmation screen.&#x20;

{% hint style="warning" %}
#### Route confirmation and market volatility

Do note that upon the "Confirm Swap" pop-up being displayed, the final route has already been secured (i.e. "locked-in) and only gas fee estimations are being refreshed based on the market rate.

In times of extreme volatility, the market conditions might have changed significantly in-between clicking the "Swap" button and the "Confirm Swap" pop-up being displayed. KyberSwap will display the latest rates in the "Confirm Swap" pop-up to reduce the likelihood that the transaction will fail.&#x20;

Please review the swap information in full prior to confirmation as the final secured route might differ from the swap screen (see [Step 3](instantly-swap-at-the-best-rates.md#step-3-configure-swap-amount)). To protect your trade, KyberSwap highly recommends that users take advantage of our "Max Slippage" feature (refer to [Cutomizing trade parameters](instantly-swap-at-the-best-rates.md#customizing-trade-parameters)).
{% endhint %}

The confirmation screen displays a few key pieces of information to review.

![Swap confirmation popup](https://support.kyberswap.com/hc/article\_attachments/13999992516249)

* Estimated return after the Swap.
* **Current Price**: the rate at which the swap will happen (this can be inverted using the 🔁 button).
* **Minimum Received**: This is the minimum amount of output tokens that you will receive from the swap. The swap will only be completed if this minimum amount threshold is achieved else the transaction will revert.
* **Gas Fee**: The estimated network fee associated with this transaction.
* **Price Impact**: The estimated change in the market price due to the size of your transaction.

{% hint style="danger" %}
#### Price impact

Do take note of the resulting price impact of your trade as this will determine the final average price of your trade. Higher trade volumes relative to available liquidity will result in each additional token unit being acquired at a higher price. As such, a higher price impact would result in subpar swap rates.
{% endhint %}

* **Slippage**: The estimated difference between the expected price and final price of the trade. Slippage is an inherent characteristic of all active markets whose risks can only be mitigated. For more detailed insights, please refer to [Slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md).

Click the “Confirm Swap” button to proceed. You should see the Transaction Submitted screen appear. You can click on "View Transaction" to see your transaction on the blockchain explorer.

![Transaction broadcasted confirmation](https://support.kyberswap.com/hc/article\_attachments/13999993296281)

You should also see the transaction appear in your account’s transaction history.

![Transaction history](https://support.kyberswap.com/hc/article\_attachments/14000001237273)

## Customizing trade parameters

<figure><img src="../../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

The KyberSwap Interface also provides additional features for more advanced traders that allow customisation of the following trade parameters:

* **Max Slippage:** The maximum amount of slippage before the trade is reverted. Slippage refers to the difference between the expected and final price at which the trade was executed. As market conditions can change between the submission and execution of the trade, this guarantees that the trade will only be executed if the final price is within the expected price interval.&#x20;

{% hint style="warning" %}
#### Max Slippage setting

While KyberSwap recommends keeping the slippage as low as possible to ensure that trades are executed at the best rates, such transactions might face a higher failure rate in times of extreme market volatility.

Setting a higher slippage increases the likelihood of transaction success but comes with greater risks of worse rates due to market volatility as well as the presence of frontrunning opportunities. **KyberSwap highly recommends setting a slippage for all swaps to protect your trades.**
{% endhint %}

* **Transaction Time Limit:** The amount of time from submission that the transaction is valid for. If the transaction is not executed within the specified time frame, the transaction will be cancelled.
* **Advanced Mode:** Toggle this button to allow for high impact trades without any confirmation prompts. Be extra careful when enabling this as large trades might result in significant slippage.
* **Liquidity Sources:** Select the liquidity sources (i.e. DEXes) through which your trade will be routed. By default, all KyberSwap supported DEXes on the connected chain will be selected.

These settings can be accessed via selecting the slider icons on the main swap page:

<figure><img src="../../../.gitbook/assets/image (87).png" alt=""><figcaption><p>Access the trading settings</p></figcaption></figure>
