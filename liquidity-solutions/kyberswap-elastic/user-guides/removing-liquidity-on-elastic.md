---
description: Another Opportunity Awaits
---

# Removing Liquidity on Elastic

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
3. [Elastic Pool Creation ](elastic-pool-creation.md)
4. [Add Liquidity To An Existing Elastic Pool ](add-liquidity-to-an-existing-elastic-pool.md)
5. [Increasing Liquidity On Elastic](increasing-liquidity-on-elastic.md)&#x20;
6. [Elastic Fee Collection](elastic-fee-collection.md)&#x20;
7. [Yield Farming On Elastic](yield-farming-on-elastic.md)&#x20;
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
#### Fee-on-transfer tokens

Certain ERC20 token smart contracts implement a fee-on-transfer (FOT) mechanism whereby for every token transfer, a percentage of the tokens are burned or distributed to various wallets. As a permissionless dapp, KyberSwap enables users to [Add Their Favourite Tokens](../../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md) and hence do not limit the type of tokens traded as long as the token follows the [ERC20 standard](https://docs.openzeppelin.com/contracts/4.x/erc20).

When adding or removing FOT tokens from an AMM pool, tokens will be transferred to and from the pool contract. Given that FOT tokens are designed to charge a tax on every transfer, each addition or removal of FOT tokens from a pool will incur a FOT tax which is usually a fixed percentage of the transfer amount.

Note that the FOT tax is specified in the FOT token's smart contract (i.e. the FOT token team) hence KyberSwap does not have any control over the FOT mechanism. Users are advised to trade such tokens at their own risk as KyberSwap was optimized to handle the standard ERC20 implementation.
{% endhint %}

### **Step 3**: Review liquidity removal

Click the “Preview” button to bring up a preview screen. Once you are satisfied with the transaction details, click the “Remove” button and then confirm this transaction on your wallet.

![Conform removal](https://support.kyberswap.com/hc/article\_attachments/14005916048153)

Note: If you have any uncollected fees, these will all be automatically collected as part of the liquidity removal transaction regardless of the amount of liquidity removed.
