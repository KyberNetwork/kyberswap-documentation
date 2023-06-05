---
description: Capital Efficient Pools With Auto-Compounding Yields
---

# Add Liquidity To An Existing Elastic Pool

## Introduction

In order to participate in a **KyberSwap Elastic** pool and earn fees, you first need to add liquidity to the pool. Adding liquidity to a pool opens a new position. You can add liquidity either to an existing pool, or as part of creating a new pool. This guide describes the steps required to **add liquidity to an existing pool**.

Note: “Adding Liquidity” should not be confused with “Increasing Liquidity.” Adding Liquidity means creating a new position, whereas Increasing Liquidity pertains to increasing the size of a position you currently hold. Please refer to [Increasing Liquidity On Elastic](increasing-liquidity-on-elastic.md) if you have an existing position that you would like to add more liquidity to.

<details>

<summary>Liquidity Provider Flow</summary>

Still deciding on which solution suits you best?&#x20;

* **Overview**: [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
* **Detailed comparison**:  [Classic vs Elastic](../../classic-vs-elastic/)&#x20;

#### Next steps

1. [Connect Your Wallet](../../../kyberswap-solutions/kyberswap-interface/user-guides/connect-your-wallet.md)
2. [Switching Networks](../../../kyberswap-solutions/kyberswap-interface/user-guides/selecting-preferred-network.md)
3. [Elastic Pool Creation ](elastic-pool-creation.md)
4. **Add Liquidity To An Existing Elastic Pool <-**
5. [Increasing Liquidity On Elastic](increasing-liquidity-on-elastic.md)
6. [Elastic Fee Collection](elastic-fee-collection.md)
7. [Yield Farming On Elastic](yield-farming-on-elastic.md)
8. [Removing Liquidity On Elastic](removing-liquidity-on-elastic.md)

</details>

## Adding liquidity to an existing pool

Here are the steps for opening a new position using an existing liquidity pool.

### **Step 1**: View available pools

Ensure you are on the correct network, and then choose the tokens to provide as liquidity. You can do this through the token selectors at the top of the Elastic Pools interface. Once you’ve selected your pair of tokens, a filtered list of pools that use that pair will be displayed on the interface.

![View available pools](https://support.kyberswap.com/hc/article\_attachments/14197115708185)

Note: If you know the contract address of the pool you want, you can also filter the list for the pool you want by inputting the address in the search bar.

### **Step 2**: Select pool

Select the pool you’d like to participate in by clicking on the appropriate “Add Liquidity” button. This will open the Add Liquidity screen.

![Add liquidity pop-up](https://support.kyberswap.com/hc/article\_attachments/14197098964249)

{% hint style="danger" %}
#### Adding liquidity to an out of range pool

For the safety of our LPs, KyberSwap Elastic will notify LPs when adding liquidity to a pool that is out of range. This is because any liquidity additions that significantly deviates from the market price would immediately result in [impermanent loss](../../../getting-started/foundational-topics/decentralized-finance/impermanent-loss.md) as arbitrageurs sweep up the significantly discounted token from the position.

![](<../../../.gitbook/assets/image (4).png>)
{% endhint %}

{% hint style="warning" %}
#### Fee-on-transfer tokens

Certain ERC20 token smart contracts implement a fee-on-transfer (FOT) mechanism whereby for every token transfer, a percentage of the tokens are burned or distributed to various wallets. As a permissionless dapp, KyberSwap enables users to [Add Their Favourite Tokens](../../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md) and hence do not limit the type of tokens traded as long as the token follows the [ERC20 standard](https://docs.openzeppelin.com/contracts/4.x/erc20).

When adding or removing FOT tokens from an AMM pool, tokens will be transferred to and from the pool contract. Given that FOT tokens are designed to charge a tax on every transfer, each addition or removal of FOT tokens from a pool will incur a FOT tax which is usually a fixed percentage of the transfer amount.

Note that the FOT tax is specified in the FOT token's smart contract (i.e. the FOT token team) hence KyberSwap does not have any control over the FOT mechanism. Users are advised to trade such tokens at their own risk as KyberSwap was optimized to handle the standard ERC20 implementation.
{% endhint %}

### **Step 3**: Select fee tier&#x20;

For a list of fee tiers and their recommended applications, please refer to [Fee Tier Options](elastic-pool-creation.md#fee-tier-options).

![Select fee tier](https://support.kyberswap.com/hc/article\_attachments/14197115918873)

### **Step 4**: Set your price range

This is the range at which your capital will be used in the pool. If the market price moves outside the range your capital will not be used and will not earn any fees.

You can set your price range either using the sliders or by typing in prices manually.

![Select price range](https://support.kyberswap.com/hc/article\_attachments/14197115971993)

Note: You can also choose to click on the “Full Price Range” option, but that will set your range to be between 0 and infinity, and your liquidity will be very thinly spread out, greatly impairing its fee-earning potential.

{% hint style="warning" %}
#### Single-sided liquidity

For the safety of our LPs, KyberSwap Elastic only allows single-sided liquidity to be added if the selected price range does not support the current market price. This is because the addition of double-sided liquidity outside the market price would immediately result in [impermanent loss](../../../getting-started/foundational-topics/decentralized-finance/impermanent-loss.md) as arbitrageurs sweep up the significantly discounted token from the position.

Whenever a position outside the market price is created, the deposit amount for the corresponding token that is prone to immediate impermanent loss is disabled.

![](<../../../.gitbook/assets/image (8).png>)
{% endhint %}

### **Step 5**: Configure token amounts

Specify the deposit amounts, or how much liquidity you would like to add to open this position. You can either manually type in amounts or use the “Max” and “Half” buttons. Once you specify the deposit amount for one leg of the pair, the corresponding leg’s amount will be automatically calculated and populated for you.

Note: The proportion of liquidity deposited for each leg of the pair is determined by your price range, so it is helpful to set the price range before specifying your deposit amounts.

![Deposit amounts](https://support.kyberswap.com/hc/article\_attachments/14197116099097)

### **Step 6**: Authorize contract

If you haven’t already done so, you will need to need to authorize the KyberSwap smart contract to transact using your tokens on this network. Click the “Approve \[Token]” button to do so. This will open the approval dialog window on your wallet.

![Approve USDC](https://support.kyberswap.com/hc/article\_attachments/14197099433625)

Once the approval is confirmed, the previously-greyed-out “Preview” button will be clickable.

### **Step 7**: Review liquidity provision

Click on the “Preview” button to bring up the preview screen. Once you have reviewed the information on this screen, click on the “Supply” button to proceed.

![Preview pop-up](https://support.kyberswap.com/hc/article\_attachments/14197099595545)

You will need to confirm this transaction in your wallet.

![Metamask confirmation](https://support.kyberswap.com/hc/article\_attachments/14197099648409)

Once you’ve confirmed the transaction you will see a screen informing you that the transaction has been submitted. You can click on “View Transaction” to view your transaction on the appropriate blockchain explorer.

![Transaction submitted](https://support.kyberswap.com/hc/article\_attachments/14197099789209)

Your new position should now be visible on the My Pools page on KyberSwap.

![Elastic pool positions](https://support.kyberswap.com/hc/article\_attachments/14197099857049)
