---
description: Another Opportunity Awaits
---

# Removing Liquidity on Elastic

## Introduction

Have you discovered an even better yield opportunity or maybe you just want to take a break from the markets. You can easily reduce the amount of liquidity within a position or exit the position completely through removing all your contributed liquidity. This guide describes the steps to remove all or part of your liquidity from a position.

{% hint style="success" %}
#### Removing liquidity for positions staked in farms

KyberSwap Elastic enables LPs to conveniently remove liquidity while their positions are staked in a farm. Staked positions are automatically withdrawn from the farms with rewards being automatically harvested.&#x20;

In a single transaction, users can unstake their position from the farm, withdraw their position from farming contract, and close their positions with tokens being directly debited to their wallet address. This time-saving feature ensures that LPs can easily readjust their positions while still maximizing their farming rewards.
{% endhint %}

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
5. [Increasing Liquidity On Elastic](increasing-liquidity-on-elastic.md)&#x20;
6. [Elastic Fee Collection](elastic-fee-collection.md)&#x20;
7. [Yield Farming On Elastic](broken-reference)&#x20;
8. **Removing Liquidity On Elastic** **<-**

</details>

## Removing liquidity positions

### **Step 1**: Select position

From the My Pools page, choose the position from which you want to remove liquidity and click on its “Remove Liquidity” button.

![Remove liquidity button](https://support.kyberswap.com/hc/article\_attachments/14005915751961)

This brings up the Remove Liquidity screen.

### **Step 2**: Specify removal amount

Specify the amount of liquidity to remove. You can do this either by using the pre-set percentage buttons or the percentage slider, or by manually typing in the amount for either leg of the pair.

![Configure liquidity removal amount](https://support.kyberswap.com/hc/article\_attachments/14005916033561)

Note: If you choose to remove 100% of the liquidity in this position, that is tantamount to closing the position. Once this operation is complete, you will only see this position if you toggle the “Show closed positions” button on your My Positions page.

{% hint style="warning" %}
#### Non-standard tokens

As a permissionless protocol, KyberSwap enables users to provide liquidity and market make for any token implementing the [ERC20](https://docs.openzeppelin.com/contracts/4.x/erc20) interface. While this standard interface enables interoperability between various DeFi protocols (including KyberSwap), token teams are still able to specify customized token mechanics (i.e. supply/demand, tokenomics, etc.) which could result in unexpected outcomes.

Note that the token mechanics are specified as part of the token's smart contract hence KyberSwap does not have any control over specific token implementations. Some examples of non-standard tokens are:

* **Fee-on-transfer (FOT)**: For every token transfer, a percentage of the tokens are burned or distributed to various wallets.&#x20;
* **Rebase**: Token supply is adjusted periodically to maintain price stability.
* **LP**: Tokens representing a proportional claim of a liquidity pool's assets.

To ensure the safety of our user's funds, KyberSwap Elastic does not support non-standard tokens. Please do your own research before providing liquidity using such tokens as KyberSwap was optimized to handle the standard ERC20 implementation.
{% endhint %}

### **Step 3**: Review liquidity removal

Click the “Preview” button to bring up a preview screen.&#x20;

{% hint style="warning" %}
#### Slippage: Protecting your liquidity

As an AMM protocol, any removal of liquidity from the pool might result in slippage whereby the final amount withdrawn differs from the expected amount. To minimize the effects of slippage, KyberSwap Elastic enables you to configure a slippage tolerance that caps the amount of slippage above which your transaction will be reverted (i.e. failed and cancelled).

![](../../../.gitbook/assets/Elastic\_RemoveLiquidity\_SlippageToleranceSetting.png)

Please refer to [AMM Slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md#amm-slippage) for further details on why slippage occurs and how to protect your liquidity additions or removals.
{% endhint %}

Once you are satisfied with the transaction details, click the “Remove” button and then confirm this transaction on your wallet.

![Conform removal](https://support.kyberswap.com/hc/article\_attachments/14005916048153)

Note: If you have any uncollected fees and/or farming rewards, these will all be automatically collected as part of the liquidity removal transaction regardless of the amount of liquidity removed.
