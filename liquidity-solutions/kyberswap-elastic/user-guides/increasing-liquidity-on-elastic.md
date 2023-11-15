---
description: Add To Your Favourite Concentrated Liquidity Positions
---

# Increasing Liquidity On Elastic

## Introduction

If you already have a KyberSwap Elastic liquidity pool position that’s doing well, you may want to increase the size of that position. This is called **Increasing Liquidity**.

Note: “Increasing Liquidity” should not be confused with “Adding Liquidity.” Adding Liquidity means creating a new position, whereas Increasing Liquidity pertains to increasing the size of a position you currently hold. Please refer to [Add Liquidity To An Existing Elastic Pool ](add-liquidity-to-an-existing-elastic-pool.md)if you would like to enter a new position.

<details>

<summary>Liquidity Provider Flow</summary>

Still deciding on which solution suits you best?&#x20;

* **Overview**: [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
* **Detailed comparison**:  [Classic vs Elastic](../../classic-vs-elastic/)&#x20;

#### Next steps

1. [Connect Your Wallet](../../../kyberswap-solutions/kyberswap-interface/user-guides/connect-your-wallet.md)
2. [Switching Networks](../../../kyberswap-solutions/kyberswap-interface/user-guides/selecting-preferred-network.md)
3. [Elastic Pool Creation ](elastic-pool-creation.md)
4. [Add Liquidity To An Existing Elastic Pool ](add-liquidity-to-an-existing-elastic-pool.md)
5. **Increasing Liquidity On Elastic** **<-**
6. [Elastic Fee Collection](elastic-fee-collection.md)
7. [Yield Farming On Elastic](broken-reference)
8. [Removing Liquidity On Elastic](removing-liquidity-on-elastic.md)

</details>

## Increasing the liquidity of an existing position

{% hint style="success" %}
:zap: **Elastic Zap** :zap:

LPs can now zap into Elastic pools! This means adding liquidity with just a single token without the complexities of sourcing the exact token ratios.

Please visit the [Elastic Zap](../concepts/elastic-zap.md) explainer on how KyberSwap is making the LP experience more convenient while minimizing position management costs and risks.

Supported on:

* Arbitrum (ChainID: 42161)
* Polygon PoS (ChainID: 137)
* Optimism (ChainID: 10)
* Avalanche (ChainID: 43114)
* Base (ChainID: 8453)
* Scroll (ChainID: 534352)
{% endhint %}

### **Step 1**: Select position

From the [My Positions page](https://scrollscan.com/address/0xf0096e5B4AAfeEA1DF557264091569ba125c1172), look for the position you’d like to increase and click its corresponding “Increase Liquidity”  of :zap:"Zap In" button.

![Position details](../../../.gitbook/assets/Elastic\_UserGuide\_IncLiq\_SelectPosition.png)

This opens up the relevant page/popup depending on whether you want to add a single token (i.e. [zap](../../../getting-started/foundational-topics/decentralized-finance/zap.md)) or two tokens.

{% tabs %}
{% tab title="Zap In" %}
<figure><img src="../../../.gitbook/assets/Elastic_UserGuide_IncLiq_ZapInPage.png" alt=""><figcaption><p>Zap In Page</p></figcaption></figure>
{% endtab %}

{% tab title="Token Pair" %}
<figure><img src="../../../.gitbook/assets/Elastic_UserGuide_IncLiq_TokenPairPage.png" alt=""><figcaption><p>Token Pair Page</p></figcaption></figure>
{% endtab %}

{% tab title="Quick Zap" %}
<figure><img src="../../../.gitbook/assets/Elastic_UserGuide_IncLiq_QuickZapPopup.png" alt=""><figcaption><p>Quick Zap Popup</p></figcaption></figure>
{% endtab %}
{% endtabs %}

### **Step 2:** Configure additional liquidity amounts

Specify the deposit amounts, or the magnitude of the position size increase. You can either manually type in amounts or use the “Max” and “Half” buttons.&#x20;

Note: The proportion of liquidity deposited for each leg of the pair is determined by the price range associated with the position.

{% tabs %}
{% tab title="Zap In" %}
<figure><img src="../../../.gitbook/assets/Elastic_UserGuide_IncLiq_ZapInAmount.png" alt=""><figcaption><p>Zap In Increment Amount</p></figcaption></figure>

You can switch which pool token that you will be zapping in with by selecting the token toggle. Once an amount has been set, you will be able to see the estimated token ratios for increment amount.

Additionally, do take note of the corresponding [slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md) and [price impact](../../../getting-started/foundational-topics/decentralized-finance/price-impact.md) as well. The slippage for the zap can be set in the dropdown menu bar on the top right.
{% endtab %}

{% tab title="Token Pair" %}
<figure><img src="../../../.gitbook/assets/Elastic_UserGuide_IncLiq_TokenPairAmount.png" alt=""><figcaption><p>Token Pair Increment Amount</p></figcaption></figure>

Once you specify the deposit amount for one leg of the pair, the corresponding leg’s amount will be automatically calculated and populated for you.
{% endtab %}

{% tab title="Quick Zap" %}
<figure><img src="../../../.gitbook/assets/Elastic_UserGuide_IncLiq_QuickZapAmount.png" alt=""><figcaption><p>Quick Zap Increment Amount</p></figcaption></figure>

You can switch which pool token that you will be zapping in with by selecting the token toggle. Once an amount has been set, you will be able to see the estimated token ratios for increment amount.

Additionally, do take note of the corresponding [slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md) and [price impact](../../../getting-started/foundational-topics/decentralized-finance/price-impact.md) as well. The slippage for the zap can be set in the dropdown menu bar on the top right.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
#### Non-standard tokens

As a permissionless protocol, KyberSwap enables users to provide liquidity and market make for any token implementing the [ERC20](https://docs.openzeppelin.com/contracts/4.x/erc20) interface. While this standard interface enables interoperability between various DeFi protocols (including KyberSwap), token teams are still able to specify customized token mechanics (i.e. supply/demand, tokenomics, etc.) which could result in unexpected outcomes.

Note that the token mechanics are specified as part of the token's smart contract hence KyberSwap does not have any control over specific token implementations. Some examples of non-standard tokens are:

* **Fee-on-transfer (FOT)**: For every token transfer, a percentage of the tokens are burned or distributed to various wallets.&#x20;
* **Rebase**: Token supply is adjusted periodically to maintain price stability.
* **LP**: Tokens representing a proportional claim of a liquidity pool's assets.

To ensure the safety of our user's funds, KyberSwap Elastic does not support non-standard tokens. Please do your own research before providing liquidity using such tokens as KyberSwap was optimized to handle the standard ERC20 implementation.
{% endhint %}

### **Step 3**: Authorize contract

If you haven’t already done so, you will need to need to authorize the KyberSwap smart contract to transact using your tokens on this network. Click the “Approve \[Token]” button to do so. This will open the approval dialog window on your wallet.

![Approve USDC](https://support.kyberswap.com/hc/article\_attachments/14196887506201)

Once the approval is confirmed, the previously-greyed-out “Preview” button will be clickable.

### **Step 4**: Review increase liquidity

Click on the “Preview” button to bring up the preview screen.&#x20;

{% hint style="warning" %}
#### Slippage: Protecting your liquidity

As an AMM protocol, any additions of liquidity to the pool might result in slippage whereby the final amount deposited differs from the expected amount. To minimize the effects of slippage, KyberSwap Elastic enables you to configure a slippage tolerance that caps the amount of slippage above which your transaction will be reverted (i.e. failed and cancelled).

![](../../../.gitbook/assets/Elastic\_IncreaseLiquidity\_SlippageToleranceSetting.png)

Please refer to [AMM Slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md#amm-slippage) for further details on why slippage occurs and how to protect your liquidity additions or removals.
{% endhint %}

Once you have reviewed the information on this screen, click on the “Supply” button to proceed.

![Increas liquidity preview](https://support.kyberswap.com/hc/article\_attachments/14196871104409)

You will need to confirm this transaction in your wallet.

![Metamask confirmation](https://support.kyberswap.com/hc/article\_attachments/14196887684249)

Once you’ve confirmed the transaction you will see a screen informing you that the transaction has been submitted. You can click on “View Transaction” to view your transaction on the appropriate blockchain explorer.

![Transaction submitted](https://support.kyberswap.com/hc/article\_attachments/14196871282457)

The newly increased position should now be visible on the My Positions page.

![New position size](https://support.kyberswap.com/hc/article\_attachments/14196887883033)
