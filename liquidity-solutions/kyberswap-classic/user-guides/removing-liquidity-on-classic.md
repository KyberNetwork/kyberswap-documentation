---
description: Another Opportunity Awaits
---

# Removing Liquidity On Classic

## Introduction

Have you discovered an even better yield opportunity or maybe you just want to take a break from the markets. You can easily reduce the amount of liquidity within a position or exit the position completely through removing all your contributed liquidity. This guide describes the steps to remove all or part of your liquidity from a position.

<details>

<summary>Liquidity Provider Flow</summary>

Still deciding on which solution suits you best?&#x20;

* **Overview**: [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
* **Detailed comparison**:  [Classic vs Elastic](../../classic-vs-elastic/)&#x20;

#### Next steps

1. [Connect Your Wallet](../../../kyberswap-solutions/kyberswap-interface/user-guides/connect-your-wallet.md)
2. [Switching Networks](../../../kyberswap-solutions/kyberswap-interface/user-guides/selecting-preferred-network.md)
3. [Classic Pool Creation ](classic-pool-creation.md)
4. [Add Liquidity To An Existing Classic Pool ](add-liquidity-to-an-existing-classic-pool.md)
5. [Yield Farming On Classic ](yield-farming-on-classic.md)
6. **Removing Liquidity On Classic <-**

</details>

## Removing liquidity position

### **Step 1**: Select position

From the My Pools page, choose the position from which you want to remove liquidity and click on its “Remove Liquidity” button.

<figure><img src="../../../.gitbook/assets/image (130).png" alt=""><figcaption><p>Classic pools dashboard</p></figcaption></figure>

This brings up the Remove Liquidity screen.

### **Step 2**: Specify removal amount

KyberSwap Classic provides LPs the option to withdraw their position as a token pair or a single token. Withdrawing to a single token (a.k.a zaps) enable users to conveniently withdraw their position's value as either token in the pool. LPs can choose to remove part or the whole position.

Note: If you choose to remove 100% of the liquidity in this position, that is tantamount to closing the position. Once this operation is complete, you will only see this position if you toggle the “Show closed positions” button on your My Positions page.

{% tabs %}
{% tab title="Token Pair" %}
<figure><img src="../../../.gitbook/assets/image (144).png" alt=""><figcaption><p>Token pair removal</p></figcaption></figure>

Specify the amount of liquidity to remove. You can do this either by using the pre-set percentage buttons or the percentage slider, or by manually typing in the amount for either leg of the pair.&#x20;
{% endtab %}

{% tab title="Single Token" %}
<figure><img src="../../../.gitbook/assets/image (73).png" alt=""><figcaption><p>Single token removal</p></figcaption></figure>

For single token removals, you can specify the percentage or exact amount of LP tokens to remove. The corresponding output token amount can be seen under the "Output".

You can also switch the output token by selecting the token under the "Output" section.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
#### Non-standard tokens

As a permissionless protocol, KyberSwap enables users to provide liquidity and market make for any token implementing the [ERC20](https://docs.openzeppelin.com/contracts/4.x/erc20) interface. While this standard interface enables interoperability between various DeFi protocols (including KyberSwap), token teams are still able to specify customized token mechanics (i.e. supply/demand, tokenomics, etc.) which could result in unexpected outcomes.

Note that the token mechanics are specified as part of the token's smart contract hence KyberSwap does not have any control over specific token implementations. Some examples of non-standard tokens are:

* **Fee-on-transfer (FOT)**: For every token transfer, a percentage of the tokens are burned or distributed to various wallets.&#x20;
* **Rebase**: Token supply is adjusted periodically to maintain price stability.
* **LP**: Tokens representing a proportional claim of a liquidity pool's assets.

To ensure the safety of our user's funds, KyberSwap Classic does not support non-standard tokens. Please do your own research before providing liquidity using such tokens as KyberSwap was optimized to handle the standard ERC20 implementation.
{% endhint %}

### Step 3: Authorize contract

If you haven't done so, you will need to permit the pool contract to remove your position from the pool. Note that this signature request does not require any gas.

<figure><img src="../../../.gitbook/assets/image (175).png" alt=""><figcaption><p>Metamask permit signature</p></figcaption></figure>

Once you have authorized the contract, the previously disabled "Remove" button will now be available.

### Step 4: Review liquidity removal

Click the "Remove" button to bring up the preview screen. The preview screen displays a few key pieces of information for review.

<figure><img src="../../../.gitbook/assets/image (146).png" alt=""><figcaption><p>Removal confirmation pop-up</p></figcaption></figure>

* Amount of tokens that you will receive after removing the position
* **Current price:** the rate at which the swap will happen (this can be inverted using the 🔁 button).
* **LP Tokens Removed:** The number of LP tokens, which represents your position, that will be removed
* **Minimum Received:** This is the minimum amount of output tokens that you will receive from the removal. The removal will only be completed if this minimum amount threshold is achieved else the transaction will revert.

{% hint style="warning" %}
#### Slippage: Protecting your liquidity

As an AMM protocol, any removal of liquidity from the pool might result in slippage whereby the final amount withdrawn differs from the expected amount. To minimize the effects of slippage, KyberSwap Classic enables you to configure a slippage tolerance that caps the amount of slippage above which your transaction will be reverted (i.e. failed and cancelled).

![](../../../.gitbook/assets/Classic\_RemoveLiquidity\_SlippageToleranceSetting.png)

Please refer to [AMM Slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md#amm-slippage) for further details on why slippage occurs and how to protect your liquidity additions or removals.
{% endhint %}

Click the “Confirm” button to proceed. You should be prompted to confirm the transaction in your wallet.

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption><p>KyberSwap pending confirmation</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (152).png" alt=""><figcaption><p>Metamask confirmation</p></figcaption></figure>

Once confirmed, the Transaction Submitted screen will appear. You can click on "View Transaction" to see your transaction on the blockchain explorer.

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption><p>Transaction submitted</p></figcaption></figure>
