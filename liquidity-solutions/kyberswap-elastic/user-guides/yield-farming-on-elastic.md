---
description: Claim Additional Elastic Rewards
---

# Yield Farming On Elastic

## Introduction

Yield Farming or Liquidity Mining is a aspect of DeFi that allows Liquidity Providers (LPs) to passively earn a return on capital contributed to a liquidity pool. The Yield Farm provides LPs with rewards over time to incentivize LPs to continue to provide liquidity to the pool as well as to help offset their risk.

This guide covers yield farming on KyberSwap Elastic. It covers the following aspects of yield farming on KyberSwap Elastic:

* [Staking Liquidity Positions](yield-farming-on-elastic.md#staking-liquidity-positions)
* [Harvesting and Claiming Rewards](yield-farming-on-elastic.md#harvesting-and-claiming-rewards)
* [Unstaking Liquidity Positions](yield-farming-on-elastic.md#unstaking-liquidity-positions)

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
7. **Yield Farming On Elastic <-**
8. [Removing Liquidity On Elastic](removing-liquidity-on-elastic.md)

</details>

## Staking liquidity positions

To be eligible to earn rewards, you will first need to stake some liquidity positions. A guide on how to do this can be found [here](add-liquidity-to-an-existing-elastic-pool.md).

### **Step 1**: Select your network

If this is your first time interacting with KyberSwap Elastic liquidity pools on this particular network, you will need to give approval for the farming smart contract to manage your wallet and balances.

Click on the “Approve Farming Contract” button on the Farms page to begin. This will require an onchain approval through your Web3 wallet.

Note: Be sure to check that the smart contract address is correct before authorizing the smart contract. KyberSwap Elastic farming smart contract addresses can be found [here](../../../reference/legacy/elastic-legacy/elastic-farming-contract-addresses.md).

![Approve farming contract](https://support.kyberswap.com/hc/article\_attachments/14231073638297)

![Metamask confirmation of authorization](https://support.kyberswap.com/hc/article\_attachments/14231073584921)

Once the approval transaction is confirmed, the green “Approve Farming Contract” button will disappear from the UI. You can now stake any farming NFTs into the farming contract to earn rewards.

### **Step 2**: Approve and add liquidity to the farm of your choice.&#x20;

For the purposes of this guide, we will use the following USDC-stMATIC pool on Polygon.

![USDC/stMATIC pool](https://support.kyberswap.com/hc/article\_attachments/14231089487385)

### **Step 3**: Deposit LP liquidity into farming contract

Deposit liquidity into the farming contract by clicking on the “Deposit” button on the Active Farms page and then selecting the NFT associated with the liquidity position that you would like to stake. Click the “Deposit Selected” button to proceed. (This is an onchain transaction.)

![Deposit to farming contract](https://support.kyberswap.com/hc/article\_attachments/14231073926425)

![Select position to deposit](https://support.kyberswap.com/hc/article\_attachments/14231089720601)

You should now see that the amount of liquidity that you have deposited into the farming contract has changed. Some farming actions will also now be enabled for the pool that you have selected.

![Deposit amount changed](https://support.kyberswap.com/hc/article\_attachments/14231074218137)

### **Step 4**: Stake your position in the farm

Click on the “+” button to stake your NFT position. Select the appropriate NFT from the list on the next screen and click the “Stake Selected” button to proceed. (This is an onchain transaction.)

![Stake position](https://support.kyberswap.com/hc/article\_attachments/14231074371737)

![Select liquidity position](https://support.kyberswap.com/hc/article\_attachments/14231090132889)

Your position is now staked and is now eligible to accumulate rewards for the duration of the farming phase. You should now also be able to see your farming pool under the “My Farms” tab. This page will also display ended phases for the farms that you are currently participating in.

Note: Depending on the [farming mechanism](https://support.kyberswap.com/hc/en-us/articles/14227778525209) associated with your farm, your rewards will be calculated depending on the value of your liquidity position staked in the farm relative to other farmers, how long your liquidity position has been active in the pool (i.e. in range), and the trading volume utilizing your active liquidity position in the pool.

![My farms](https://support.kyberswap.com/hc/article\_attachments/14231090279577)

## Harvesting and claiming rewards

After you have accumulated rewards, you can harvest them from the pool and subsequently claim them (i.e. withdraw rewards to your wallet).

### **Step 1**: Select pools to harvest

From the Farms page, click on the small “pickaxe” button associated with your desired pool to bring up the Harvest screen. Alternatively, if you have multiple pool farms and would like to harvest them all at once, you can use the “Harvest All” button to batch all the harvest transactions together. Please note that this does not save you any gas fees since every individual harvest call of the smart contract still needs to be broadcasted to the blockchain.

![Harvest button](https://support.kyberswap.com/hc/article\_attachments/14231075605145)

### Step 2: Confirm harvest

From the Harvest screen that appears, click on the “Harvest” button to proceed. This is an onchain transaction that will require wallet confirmation.

![Harvest all pop-up](https://support.kyberswap.com/hc/article\_attachments/14231075539993)

If the pool does not have a rewards vesting schedule, your rewards will automatically be sent to your wallet. But if the pool has a vesting schedule, you will need to wait some time after harvesting for the rewards to vest before you can claim them.

### **Step 3**: Claim vested rewards (vested pools only)

This step only applies to certain pools with a vesting schedule for rewards. Rewards harvested from such pools will need to be claimed in a separate action. Click the “Claim” button in the Vesting tab of the Farms page.

![Claim vested rewards](https://support.kyberswap.com/hc/article\_attachments/14231075841049)

Note: The vast majority of active yield farming pools on KyberSwap do not have a vesting schedule, and these do not require this separate claim step.

## Unstaking liquidity positions

If a farming phase ends and a new phase begins, you will first need to unstake your liquidity position from the pool and re-stake it in order to resume accumulation of rewards. You may also choose to unstake from a farming pool at any time, even while the pool is still active.

### **Step 1: Select pool to unstake**

On the Farms page, click on the “-” button of the pool you would like to unstake from.

![Unstake LP token](https://support.kyberswap.com/hc/article\_attachments/14231072707993)

### Step 2: Confirm unstake

On the screen that opens, select the liquidity position(s) that you would like to unstake and then click the “Unstake Selected” button. This is an onchain transaction.

![Select position](https://support.kyberswap.com/hc/article\_attachments/14231072647321)

As part of this action, any as-yet unharvested rewards will also automatically be harvested.

From this point on, your liquidity position can either once again be staked into an active phase of the pool to earn rewards, or it can be withdrawn entirely from the farming contract.

### **Step 3**: Withdraw from farming contract&#x20;

If you no longer want to participate in the farm, you can withdraw your liquidity from the farming contract. Click the “Withdraw” button on the Farms page. From the screen that appears, select the liquidity positions to withdraw and click the “Withdraw Selected” button. This is an onchain transaction.

![Withdraw button](https://support.kyberswap.com/hc/article\_attachments/14231411355417)

![Withdraw selected position](https://support.kyberswap.com/hc/article\_attachments/14231411319449)

Note: You can only withdraw liquidity positions that have already been unstaked. Staked positions will be greyed out and unselectable.
