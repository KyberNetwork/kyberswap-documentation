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
2. [Switching Networks ](selecting-preferred-network.md)
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

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-12 at 12.23.58 PM.png" alt=""><figcaption><p>Connected chain and wallet</p></figcaption></figure>

### **Step 2:** Specify your swap pair

&#x20;You can either do this manually using the individual token selection buttons on the swap screen.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-12 at 12.27.26 PM.png" alt=""><figcaption><p>Specify tokens individually</p></figcaption></figure>

or by searching for your desired swap pair using the search field. (The keyboard shortcut Ctrl+K also opens this search feature.)

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-12 at 12.28.37 PM.png" alt=""><figcaption><p>Swap via smart search</p></figcaption></figure>

### **Step 3**: Configure swap amount

Specify the amount you would like to swap by either typing in an amount manually or by using the “Max” and “Half” buttons to swap pre-set proportions of your wallet balance. An estimate of the amount returned should appear in the quote field.

KyberSwap Interface allows users to customize trade parameters which enables greater trade security or even more advanced trade strategies. Refer to [Customizing trade parameters](instantly-swap-at-the-best-rates.md#customizing-trade-parameters) section for more details.

{% hint style="info" %}
#### Route refresh: Ensuring the best rates

Do note that the KyberSwap Interface will continuously update the swap rates in order to source the best rates for your swap given the changing market conditions. As such, you will always be able to see the latest proposed route and rates prior to clicking the "Swap" button.

Upon clicking the "Swap" button, KyberSwap Aggregator will attempt to secure the final route that will be displayed on the "Confirm Swap" pop-up (see [Step 5](instantly-swap-at-the-best-rates.md#step-5-confirm-the-swap)).
{% endhint %}

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-12 at 12.30.23 PM.png" alt=""><figcaption><p>Specify swap amount</p></figcaption></figure>

{% hint style="danger" %}
#### Max slippage: Protecting your trades

KyberSwap enables you to avoid any negative trade outcomes by setting a Max Slippage. Please refer to [Customizing trade parameters](instantly-swap-at-the-best-rates.md#customizing-trade-parameters) below for further details or [Slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md) if you would like to understand the concept better.
{% endhint %}

### **Step 4**: Approve contract to swap tokens

Approve KyberSwap to swap the tokens on your behalf. Proceed to [Step 5](instantly-swap-at-the-best-rates.md#step-5-confirm-the-swap) if token approval is not required.

If this is the first time you are swapping this token on this network using this wallet, the "Swap" button will be greyed out. You will first need to approve the KyberSwap smart contract to spend your tokens before proceeding with the swap.

Click on the "Approve \[Token]" button to begin this process. Your wallet will prompt you to give your approval for the KyberSwap smart contract to transact using this token on this network. This is a one-time action and subsequent swaps involving this token will not require further approvals unless there is an update to the smart contract.

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Approve ERC20 tokens</p></figcaption></figure>

### **Step 5**: Confirm the swap

Click the “Swap” button to bring up the confirmation screen.&#x20;

{% hint style="warning" %}
#### Route confirmation and market volatility

Do note that once the final route has been secured, the details related to your swap will be available for your review in the "Confirm Swap Details" pop-up.

In times of volatility, the market conditions might have changed in-between clicking the "Swap" button and the "Confirm Swap Details" pop-up being displayed. KyberSwap will display the latest rates in the "Confirm Swap Details" pop-up for you to review.

**If there is a change in the price, to protect you, you will need to accept the new price before proceeding with the swap. Refer tabs below for the various scenarios.**

Please review the swap information in full prior to confirmation as the final secured route might differ from the swap screen (see [Step 3](instantly-swap-at-the-best-rates.md#step-3-configure-swap-amount)). As an additional safeguard, KyberSwap highly recommends that users take advantage of our "Max Slippage" feature (refer to [Customizing trade parameters](instantly-swap-at-the-best-rates.md#customizing-trade-parameters)).
{% endhint %}

#### Price changes (==, ++, --)

{% tabs %}
{% tab title="No change in price" %}
If there are no changes to the swap price between viewing the route and confirming the route, the UI will display the following "Confirm Swap Details" pop-up.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-12 at 12.33.24 PM.png" alt=""><figcaption><p>Confirm swap with no change in price</p></figcaption></figure>
{% endtab %}

{% tab title="Better price" %}
In the case whereby the market has moved in the trader's favor, the "Confirm Swap Details" pop-up will display the greater amount and users can proceed with the swap. The user can continue to swap at even better rates thanks to KyberSwap sourcing the most optimal and updated route.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-11 at 6.26.02 PM.png" alt=""><figcaption><p>Confirm swap with better rates</p></figcaption></figure>
{% endtab %}

{% tab title="Worse price" %}
In cases whereby market conditions have moved against the trader, KyberSwap will display various warnings depending on the severity of the price deviation. To protect our users, additional safeguards are put in place to ensure that users are always in full control of their trades.&#x20;

#### Price drops by less than 1% (price drop <1%)

A warning is displayed but no additional steps are required to confirm the swap.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-11 at 6.20.23 PM.png" alt=""><figcaption><p>Confirm swap for price drop &#x3C; 1%</p></figcaption></figure>

#### Price drops more than 1% but less than 5% (1%< price drop < 5%)

A warning is displayed and user will have to accept the new amount by clicking on the "Accept New Amount" button.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-11 at 6.18.25 PM.png" alt=""><figcaption><p>Accept new amount for 1% &#x3C; price drop &#x3C; 5%</p></figcaption></figure>

#### Price drops more than 5% but less than 10% (5%< price drop < 10%)

A strong warning is displayed and user will have to accept the new amount by clicking on the "Accept New Amount" button.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-11 at 6.21.54 PM.png" alt=""><figcaption><p>Accept new amount for 5% &#x3C; price drop &#x3C; 10%</p></figcaption></figure>

#### Price drops more than 10% (10%< price drop)

A warning is displayed and user will have to accept the new amount by clicking on the "Accept New Amount" button. Additionally, users will have to manually type in their confirmation to validate that they consent to the significant price deviation.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-11 at 6.23.34 PM.png" alt=""><figcaption><p>Accept new amount for price drop &#x3C; 10%</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-11 at 6.43.19 PM.png" alt=""><figcaption><p>Manual confirmation of price drop greater than 10%</p></figcaption></figure>
{% endtab %}
{% endtabs %}

In all the above cases, the confirmation screen will always display a few key pieces of information for review:

* Estimated return after the Swap.
* **Current Price**: the rate at which the swap will happen (this can be inverted using the 🔁 button).
* **Minimum Received**: This is the minimum amount of output tokens that you will receive from the swap. The swap will only be completed if this minimum amount threshold is achieved else the transaction will revert.
* **Gas Fee**: The estimated network fee associated with this transaction.
* **Price Impact**: The estimated change in the market price due to the size of your transaction.

{% hint style="danger" %}
#### Price impact

Do take note of the resulting price impact of your trade as this will determine the final average price of your trade. Higher trade volumes relative to available liquidity will result in each additional token unit being acquired at a higher price. As such, a higher price impact would result in subpar swap rates.

Please refer to the [Price Impact](../../../getting-started/foundational-topics/decentralized-finance/price-impact.md) page for further details.
{% endhint %}

* **Slippage**: The estimated difference between the expected price and final price of the trade. Slippage is an inherent characteristic of all active markets whose risks can only be mitigated. For more detailed insights, please refer to [Slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md).

Click the “Confirm Swap” button to proceed. You should see the Transaction Submitted screen appear. You can click on "View Transaction" to see your transaction on the blockchain explorer. Additionally, you can add the token to MetaMask if you haven't already done so.

<figure><img src="../../../.gitbook/assets/image (5) (3).png" alt=""><figcaption><p>Transaction broadcasted confirmation</p></figcaption></figure>

You should also see the transaction appear in your account’s transaction history.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-12 at 12.58.30 PM.png" alt=""><figcaption><p>Transaction history in the KyberSwap wallet UI</p></figcaption></figure>

## Customizing trade parameters

<figure><img src="../../../.gitbook/assets/image (6) (3).png" alt=""><figcaption><p>Advanced swap settings</p></figcaption></figure>

The KyberSwap Interface also provides additional features for more advanced traders that allow customisation of the following trade parameters:

* **Max Slippage:** The maximum amount of slippage before the trade is reverted. Slippage refers to the difference between the expected and final price at which the trade was executed. As market conditions can change between the submission and execution of the trade, this guarantees that the trade will only be executed if the final price is within the expected price interval. For more details on slippage, refer to our [Foundational Topics](../../../getting-started/foundational-topics/decentralized-finance/slippage.md).

{% hint style="warning" %}
#### Max Slippage setting

While KyberSwap recommends keeping the Max Slippage as low as possible to ensure that trades are executed at the best rates, such transactions might face a higher failure rate in times of extreme market volatility.

Setting a higher Max slippage increases the likelihood of transaction success but comes with greater risks of worse rates due to market volatility as well as the presence of frontrunning opportunities. **KyberSwap highly recommends setting a Max Slippage for all swaps to protect your trades.**
{% endhint %}

* **Transaction Time Limit:** The amount of time from submission that the transaction is valid for. If the transaction is not executed within the specified time frame, the transaction will be cancelled.
* **Degen Mode:** Refer to [Degen Mode](instantly-swap-at-the-best-rates.md#degen-mode-tread-carefully) section below.
* **Liquidity Sources:** Select the liquidity sources (i.e. DEXes) through which your trade will be routed. By default, all KyberSwap supported DEXes on the connected chain will be selected. You can view the list of supported DEXs on each chain on the [Supported Exchanges And Networks Page](../../../getting-started/supported-exchanges-and-networks.md).

These settings can be accessed via selecting the slider icons on the main swap page:

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-12 at 1.01.34 PM.png" alt=""><figcaption><p>Access trade settings</p></figcaption></figure>

## Degen Mode: Tread carefully

KyberSwap implemented Degen Mode for our most "advanced" apes. While KyberSwap has consistently iterated upon industry-leading safeguards to enable our users to trade safely, we are aware that some advanced traders might find these protective features inconvenient. As such, switching to Degen Mode allows users to conduct high impact trades without any confirmation prompts nor price impact limits.

{% hint style="info" %}
#### Price deviations

Note that even with Degen Mode turned on, any significant price deviations that occurs while the swap is being secured will still require user confirmation. Please refer to [Route confirmation and market volatility](instantly-swap-at-the-best-rates.md#step-5-confirm-the-swap) for more details.
{% endhint %}

### Overriding safeguards

By turning on Degen Mode, multiple safeguards will be overridden allowing users to:

* Configure max slippage ≥ 20% and ≤ 50%
* Confirm trades with price impact ≥10%
* Proceed with swaps when price impact is unable to be calculated

### Activating Degen Mode

{% hint style="danger" %}
#### Advanced traders only

Tread carefully when turning on Degen Mode as [slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md) and [price impact](../../../getting-started/foundational-topics/decentralized-finance/price-impact.md) risks are not conservatively capped which could result in significant losses. **KyberSwap recommends that users only activate Degen Mode if you are fully aware of the risks of unprotected trades.**
{% endhint %}

Degen Mode can be toggled on via the "[Advanced Settings](instantly-swap-at-the-best-rates.md#customizing-trade-parameters)" pop-up covered in the previous section.

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Degen Mode toggle</p></figcaption></figure>

Upon toggling the Degen Mode switch, you will be prompted to manually confirm the switch.

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption><p>Confirm Degen Mode</p></figcaption></figure>

As a safety precaution, Degen Mode will be auto-disabled after 30 minutes of being switched on.
