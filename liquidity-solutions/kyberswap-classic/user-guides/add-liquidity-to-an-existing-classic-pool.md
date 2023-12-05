---
description: Capital Efficient Pools And Dynamic Fees
---

# Add Liquidity To An Existing Classic Pool

KyberSwap is fully permissionless, meaning anyone can create a liquidity pool or add liquidity (add tokens) to existing pools, while any Dapp, aggregator, or end user can access this liquidity. Refer to [Earn Yield by Contributing Liquidity ](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)page if you would like to know more about the various ways that you can generate yield by contributing towards this open financial infrastructure.

## Introduction

In order to participate in a **KyberSwap Classic** pool and earn fees, you first need to add liquidity to the pool. Adding liquidity to a pool opens a new position. You can add liquidity either to an existing pool, or as part of creating a new pool. This guide describes the steps required to **add liquidity to an existing pool**.

<details>

<summary>Liquidity Provider Flow</summary>

Still deciding on which solution suits you best?&#x20;

* **Overview**: [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
* **Detailed comparison**:  [Classic vs Elastic](../../classic-vs-elastic/)&#x20;

#### Next steps

1. [Connect Your Wallet](../../../kyberswap-solutions/kyberswap-interface/user-guides/connect-your-wallet.md)
2. [Switching Networks](../../../kyberswap-solutions/kyberswap-interface/user-guides/selecting-preferred-network.md)
3. [Classic Pool Creation ](classic-pool-creation.md)
4. **Add Liquidity To An Existing Classic Pool** **<-**
5. [Yield Farming On Classic](yield-farming-on-classic.md)
6. [Removing Liquidity On Classic](removing-liquidity-on-classic.md)

</details>

## Adding liquidity to an existing pool

Here are the steps for opening a new position using an existing liquidity pool.

### **Step 1**: View available pools

Ensure you are on the [correct network](../../../kyberswap-solutions/kyberswap-interface/user-guides/selecting-preferred-network.md), and then choose the tokens to provide as liquidity. You can do this through the token selectors at the top of the Classic Pools interface. Once you’ve selected your pair of tokens, a filtered list of pools that use that pair will be displayed on the interface.

![Search token pairs](https://support.kyberswap.com/hc/article\_attachments/14431174298009)

Note: If you know the contract address of the pool you want, you can also filter the list for the pool you want by inputting the address in the search bar.

### **Step 2**: Select pool

Select the pool you’d like to participate in by clicking on the appropriate “Add Liquidity” button (in card view) or the “+” button (in list view). This will open the Add Liquidity screen.

![Add liquidity popup](https://support.kyberswap.com/hc/article\_attachments/14431174295705)

From here you have two options: either deposit double-sided liquidity or single-sided liquidity.

{% hint style="danger" %}
#### Adding liquidity to an out of range pool

For the safety of our LPs, KyberSwap Classic will highlight pools which are out of range with the caution icon on the pool card.

![](<../../../.gitbook/assets/image (110).png>)

This is because any liquidity additions that significantly deviates from the market price would immediately result in [impermanent loss](../../../getting-started/foundational-topics/decentralized-finance/impermanent-loss.md) as arbitrageurs sweep up the significantly discounted token from the position.

![](<../../../.gitbook/assets/image (62).png>)
{% endhint %}

{% hint style="warning" %}
#### Non-standard tokens

As a permissionless protocol, KyberSwap enables users to provide liquidity and market make for any token implementing the [ERC20](https://docs.openzeppelin.com/contracts/4.x/erc20) interface. While this standard interface enables interoperability between various DeFi protocols (including KyberSwap), token teams are still able to specify customized token mechanics (i.e. supply/demand, tokenomics, etc.) which could result in unexpected outcomes.

Note that the token mechanics are specified as part of the token's smart contract hence KyberSwap does not have any control over specific token implementations. Some examples of non-standard tokens are:

* **Fee-on-transfer (FOT)**: For every token transfer, a percentage of the tokens are burned or distributed to various wallets.&#x20;
* **Rebase**: Token supply is adjusted periodically to maintain price stability.
* **LP**: Tokens representing a proportional claim of a liquidity pool's assets.

To ensure the safety of our user's funds, KyberSwap Classic does not support non-standard tokens. Please do your own research before providing liquidity using such tokens as KyberSwap was optimized to handle the standard ERC20 implementation.
{% endhint %}

### **Step 3**: Configure token amounts for liquidity provision

{% tabs %}
{% tab title="Double-Sided Liquidity" %}
To deposit double-sided liquidity, make sure “Token Pair” is selected on the toggle at the top of the screen, then specify the amounts you would like to deposit. You can either manually type in amounts or use the “Max” and “Half” buttons. Once you specify the deposit amount for one leg of the pair, the corresponding leg’s amount will be automatically calculated and populated for you.

![Two sided deposit](https://support.kyberswap.com/hc/article\_attachments/14431128365593)
{% endtab %}

{% tab title="Single-Sided Liquidity (a.k.a. zaps)" %}
To deposit single-sided liquidity, make sure “Single Token” is selected on the toggle at the top of the screen, then specify the token and the amount you would like to deposit. You can either manually type in the amount or use the “Max” and “Half” buttons.

Note: If you choose single-sided, in the final step, KyberSwap will automatically swap the appropriate amount of your deposited token so that your liquidity contribution is balanced between the two legs. You can see a preview of your final pool allocation on the screen.

![Single sided deposit](https://support.kyberswap.com/hc/article\_attachments/14431128368025)

Note: The proportion of liquidity deposited for each leg of the pair is automatically determined based on the current ratio of the pool.
{% endtab %}
{% endtabs %}

### **Step 4**: Authorize contract

If you haven’t already done so, you will need to need to authorize the KyberSwap smart contract to transact using your tokens on this network. Click the “Approve \[Token]” button to do so. This will open an approval dialog window on your wallet. You might need to do this twice if you’re depositing two-sided liquidity involving two tokens that require authorization.

![MetaMask approve token](https://support.kyberswap.com/hc/article\_attachments/14431174533657)

Once the approvals are confirmed, the previously-greyed-out “Supply” button will be clickable.

### **Step 5**: Review liquidity provision

Click on the “Supply” button to bring up the preview screen.&#x20;

{% hint style="warning" %}
#### Slippage: Protecting your liquidity

As an AMM protocol, any addition of liquidity to the pool might result in slippage whereby the final amount deposited differs from the expected amount. To minimize the effects of slippage, KyberSwap Classic enables you to configure a slippage tolerance that caps the amount of slippage above which your transaction will be reverted (i.e. failed and cancelled).

![](../../../.gitbook/assets/Classic\_AddLiquidity\_SlippageToleranceSetting.png)

Please refer to [AMM Slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md#amm-slippage) for further details on why slippage occurs and how to protect your liquidity additions or removals.
{% endhint %}

Once you have reviewed the information on this screen, click on the “Supply” button to proceed.

![Supply preview](https://support.kyberswap.com/hc/article\_attachments/14431128463257)

You will need to confirm this transaction in your wallet.

![MetaMask transaction confirmation](https://support.kyberswap.com/hc/article\_attachments/14431174633625)

Once you’ve confirmed the transaction you will see a screen informing you that the transaction has been submitted. You can click on “View Transaction” to view your transaction on the appropriate blockchain explorer.

![Transaction submission confirmation popup](https://support.kyberswap.com/hc/article\_attachments/14431174635929)

Your new position should now be visible on the My Pools page on KyberSwap which displays all your active KyberSwap Classic pools

![My Pools dashboard](https://support.kyberswap.com/hc/article\_attachments/14431128694169)
