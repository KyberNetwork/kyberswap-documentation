---
description: Claim Additional Classic Rewards
---

# Yield Farming On Classic

## Introduction

Yield Farming or Liquidity Mining is a aspect of DeFi that allows Liquidity Providers (LPs) to passively earn a return on capital contributed to a liquidity pool. The Yield Farm provides LPs with rewards over time to incentivize LPs to continue to provide liquidity to the pool as well as to help offset their risk.&#x20;

This guide covers yield farming on KyberSwap Classic. It covers the following aspects of yield farming on KyberSwap Classic:

* [Staking LP Tokens](yield-farming-on-classic.md#staking-lp-tokens)
* [Harvesting and Claiming Rewards](yield-farming-on-classic.md#harvesting-and-claiming-rewards)
* [Unstaking LP Tokens](yield-farming-on-classic.md#unstaking-lp-tokens)

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
5. **Yield Farming On Classic** **<-**
6. [Removing Liquidity On Classic](removing-liquidity-on-classic.md)

</details>

## Staking LP tokens

### **Step 1**: Create a Classic liquidity position

Approve and add liquidity to the farm of your choice. A guide on how to do this can be found [here](add-liquidity-to-an-existing-classic-pool.md). For the purposes of this guide, we will use the following USDC-miMATIC pool on Polygon PoS.

![Add liquidity popup](https://support.kyberswap.com/hc/article\_attachments/14434517571737)

### **Step 2**: Select farming pool

From the Active tab on the Classic Farms page, click on the “+” button associated with your selected farming pool to bring up the Stake window.

![Classic liquidity positions](https://support.kyberswap.com/hc/article\_attachments/14434517569817)

The Stake window should show you the balance you have in the pool.&#x20;

### Step 3: Approve farming contract

Click on the “Approve” button on the Stake window to give the farming smart contract permission to stake your LP tokens.

![Enable KyberSwap to stake LP tokens](https://support.kyberswap.com/hc/article\_attachments/14434565393177)

This is an onchain transaction that will require confirmation in your web3 wallet.

![Confirm staking permission](https://support.kyberswap.com/hc/article\_attachments/14434517763097)

### **Step 4**: Specify stake amount&#x20;

From the Active tab on the Classic Farms page, click on the “+” button once more to bring up the Stake window. Now that you have given the farming smart contract permission to access your LP tokens, the Stake window should look different. You can now specify the amount of LP tokens to stake either by manually typing in an amount or by using the “max” and “half” buttons.&#x20;

![Configure amount of LP tokens to stake](https://support.kyberswap.com/hc/article\_attachments/14434517918489)

### Step 5: Confirm farming transaction

Click the “Stake” button to proceed. This is an onchain transaction that will require confirmation in your web3 wallet.

![Confirm stake amount](https://support.kyberswap.com/hc/article\_attachments/14434565582361)

Once you’ve confirmed the transaction you will see a screen informing you that the transaction has been submitted. You can click on “View Transaction” to view your transaction on the appropriate blockchain explorer.

![Transaction submitted](https://support.kyberswap.com/hc/article\_attachments/14434518052761)

Your LP tokens are now staked and you are eligible to accumulate rewards for as long as your LP tokens remain staked. You should now also be able to see your farming pool under the “My Farms” tab.

![My Classic Farms page](https://support.kyberswap.com/hc/article\_attachments/14434565742105)

## Harvesting and claiming rewards

After you have accumulated rewards, you can harvest them from the pool and subsequently claim them (i.e. withdraw rewards to your wallet).

### **Step 1**: Select pools to harvest

From the Farms page, click on the small “pickaxe” button associated with your desired pool to bring up the Harvest screen. Alternatively, if you have multiple pool farms and would like to harvest them all at once, you can use the “Harvest All” button to batch all the harvest transactions together. Please note that this does not save you any gas fees since every individual harvest call of the smart contract still needs to be broadcasted to the blockchain.

![Harvest buttons](https://support.kyberswap.com/hc/article\_attachments/14434519637785)

### Step 2: Confirm harvest

From the Harvest (or Harvest All) screen that appears, click on the “Harvest” button to proceed. This is an onchain transaction that will require wallet confirmation.

![Harvest confirmation](https://support.kyberswap.com/hc/article\_attachments/14434519636889)

If the pool does not have a rewards vesting schedule, your rewards will automatically be sent to your wallet. Alternatively, if the pool has a vesting schedule, you will need to wait some time after harvesting for the rewards to vest before you can claim them.

### **Step 3**: Claim vested rewards **(vested pools only)**

This step only applies to certain pools with a vesting schedule for rewards. Rewards harvested from such pools will need to be claimed in a separate action following the end of the vesting period. To harvest such rewards, click the “Claim” button in the Vesting tab of the Farms page.

![Vesting screen](https://support.kyberswap.com/hc/article\_attachments/14434567415705)

Note: The vast majority of active yield farming pools on KyberSwap do not have a vesting schedule and as such do not require this separate claim step.

## Unstaking LP tokens

You may also choose to unstake your LP Tokens from a farming pool at any time. This will return LP tokens to your wallet and you will cease earning liquidity mining rewards from the pool. On the other hand, this will free up your liquidity in the pool and you will once again be able to withdraw the tokens representing your liquidity position.

### **Step 1**: Select pool to unstake

On the Farms page, click on the “-” button of the pool you would like to unstake LP tokens from.&#x20;

![Unstake LP token](https://support.kyberswap.com/hc/article\_attachments/14434566384409)

### Step 2: Select unstake amount

On the screen that opens, specify the amount of LP tokens you would like to unstake, and then click the “Unstake” button.&#x20;

![Specify unstake amount and confirm](https://support.kyberswap.com/hc/article\_attachments/14434566368793)

### Step 3: Confirm unstake

This is an onchain transaction. As part of this action, any as-yet unharvested rewards will also automatically be harvested.
