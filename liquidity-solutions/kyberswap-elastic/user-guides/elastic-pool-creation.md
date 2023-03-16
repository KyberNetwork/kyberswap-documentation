---
description: Create A Concentrated Liquidity Pool With Custom Fees
---

# Elastic Pool Creation

## Introduction

In order to participate in a **KyberSwap Elastic** pool and earn fees, you first need to add liquidity to the pool. Adding liquidity to a pool opens a new position. You can add liquidity either to an existing pool, or as part of creating a new pool. This guide describes the steps required to **create a new pool by adding liquidity**.

Note: “Adding Liquidity” should not be confused with “Increasing Liquidity.” Adding Liquidity means creating a new position, whereas Increasing Liquidity pertains to increasing the size of a position you currently hold. You can refer to [Add Liquidity To An Existing Elastic Pool](add-liquidity-to-an-existing-elastic-pool.md) for a guide on increasing your liquidity position.

<details>

<summary>Liquidity Provider Flow</summary>

Still deciding on which solution suits you best?&#x20;

* **Overview**: [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
* **Detailed comparison**:  [Classic vs Elastic](../../classic-vs-elastic/)&#x20;

#### Next steps

1. [Connect Your Wallet](../../../kyberswap-solutions/kyberswap-interface/user-guides/connect-your-wallet.md)
2. [Switching Networks](../../../kyberswap-solutions/kyberswap-interface/user-guides/selecting-preferred-network.md)
3. **Elastic Pool Creation <-**
4. [Add Liquidity To An Existing Elastic Pool ](add-liquidity-to-an-existing-elastic-pool.md)
5. [Increasing Liquidity On Elastic](increasing-liquidity-on-elastic.md)
6. [Elastic Fee Collection](elastic-fee-collection.md)
7. [Yield Farming On Elastic](yield-farming-on-elastic.md)
8. [Removing Liquidity On Elastic](removing-liquidity-on-elastic.md)

</details>

## Adding liquidity to create a new pool

Here are the steps to create a new pool and by definition, to open a new position.

### **Step 1**: Create a pool

Ensure you are on the correct network, and then click the “Create Pool” button at the top right of the screen.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-02-22 at 5.29.01 PM.png" alt=""><figcaption><p>Elastic Pool page</p></figcaption></figure>

This will bring up the Add Liquidity screen, but it will be fairly empty until the parameters of the pool are properly specified.

<figure><img src="../../../.gitbook/assets/image (90).png" alt=""><figcaption><p>Pool creation screen</p></figcaption></figure>

### **Step 2**: Select tokens to add

Select the pair of tokens you would like to create the pool with. You can choose from already whitelisted tokens or [import any token](../../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md) on your chosen network.

#### Note on pool initilization for low-decimal, high-value tokens

As an open and permissionless protocol, KyberSwap Elastic allows any ERC20 token pool to be created. Consequently, **users are responsible for checking the decimals of exotic tokens** as providing low-decimal but high unit value tokens might result in higher than expected pool initialization costs.&#x20;

This is due to a small portion of the provided liquidity being allocated to meet the minimum liquidity requirements when creating a new [reinvestment curve](../concepts/reinvestment-curve.md). While care has been taken when designing this anti-spam mechanism to suit the vast majority of tokens, token teams are still free to define their own tokens. Please refer to [Pool Initialization](../concepts/pool-process-flows.md#pool-unlocking--initialization) for further details.

<figure><img src="../../../.gitbook/assets/image (93).png" alt=""><figcaption><p>Select token pair</p></figcaption></figure>

### **Step 3:** Select fee tier

With the token pair selected, you will then be required to select your fee tier.&#x20;

<figure><img src="../../../.gitbook/assets/image (94).png" alt=""><figcaption><p>Select fee tier</p></figcaption></figure>

KyberSwap currently offers the following tiers to cater for different token pair correlations:

<details>

<summary><strong>Fee tier options</strong></summary>

1. **0.008% fee tier: Best for very stable pairs**\
   ****The 0.008% fee tier is ideal for token pairs that typically trade at a fixed or extremely high correlated rate, such as pairs of stablecoins (e.g. DAI-USDC). Liquidity providers take on minimal price risk in these pools, and traders expect to pay minimal fees.
2. **0.01% fee tier: Best for very stable pairs**\
   ****The 0.01% fee tier is ideal for token pairs that typically trade at a fixed or extremely high correlated rate, such as pairs of stablecoins (e.g. DAI-USDC). Liquidity providers take on minimal price risk in these pools, and traders expect to pay minimal fees.
3. **0.04% fee tier: Best for stable pairs**\
   ****The 0.04% fee tier is ideal for token pairs that typically trade at a fixed or highly correlated rate, such as pairs of stablecoins (e.g. DAI-USDC). Liquidity providers take on minimal price risk in these pools, and traders expect to pay minimal fees.
4. **0.3% fee tier: Best for most pairs**\
   ****The 0.30% fee tier is best suited for less correlated token pairs such as the ETH-DAI token pair, which are subject to significant price movements to either upside or downside. This higher fee is more likely to compensate liquidity providers for the greater price risk that they take on relative to stablecoin LPs.
5. **1% fee tier: Best for exotic pairs**\
   ****The 1% fee tier is best suited for even less correlated token pairs such as the ETH-KNC token pair, which are subject to significant price movements to either upside or downside. This higher fee is more likely to compensate liquidity providers for the greater price risk that they take on relative to stablecoin liquidity providers.

</details>

### **Step 4**: Set price range

This is the range at which your capital will be used in the pool. If the market price moves outside the range your capital will not be used and will not earn any fees.

You can set your price range either using the sliders or by typing in prices manually.

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Select price range</p></figcaption></figure>

For convenience, KyberSwap also provides you the option to choose from a list of preset ranges which correspond to different DeFi familiarity and risk profiles. The section below provides some guidance on the percentage-based options matched to the token pair correlation which is calculated by KyberSwap.

<details>

<summary>Full Range</summary>

**All token pairs:** Suitable for pairs with high price volatility. Although you always earn fees, your capital efficiency is the lowest among all choices.

</details>

<details>

<summary>Safe</summary>

**Exotic:** Suitable for high-risk appetite LPs for pairs with high price volatility. Anticipating price to fluctuate within \~150%. You can earn fees even if the price goes up by 75% or goes down by 75%.

**Normal:** Suitable for pairs with low price volatility. Anticipating price to fluctuate within \~45%. You can earn fees even if the price goes up by 22.5% or goes down by 22.5%.

**Stable:** Suitable for stablecoin or stable correlated pairs. Anticipating price to fluctuate within \~3%. You can earn fees even if the price goes up by 1.5% or goes down by 1.5%.

**Super stable:** Suitable for stable pairs. Anticipating price to fluctuate within \~1.5%. You can earn fees even if the price goes up by 0.75% or goes down by 0.75%.

</details>

<details>

<summary>Common</summary>

**Exotic:** Suitable for low-risk appetite LPs for pairs with high price volatility. Anticipating price to fluctuate within \~100%. You can earn fees even if the price goes up by 50% or goes down by 50%.

**Normal:** Suitable for pairs with low price volatility. Anticipating price to fluctuate within \~30%. You can earn fees even if the price goes up by 15% or goes down by 15%.

**Stable:** Suitable for stablecoin or stable correlated pairs. Anticipating price to fluctuate within \~2%. You can earn fees even if the price goes up by 1% or goes down by 1%.

**Super stable:** Suitable for stable pairs. Anticipating price to fluctuate within \~1%. You can earn fees even if the price goes up by 0.5% or goes down by 0.5%.

</details>

<details>

<summary>Expert</summary>

**Exotic:** Suitable for stable pairs. Anticipating price to fluctuate within \~1%. You can earn fees even if the price goes up by 0.5% or goes down by 0.5%.

**Normal:** Suitable for pairs with low price volatility. Anticipating price to fluctuate within \~9%. You can earn fees even if the price goes up by 4.5% or goes down by 4.5%.

**Stable:** Suitable for stablecoin or stable correlated pairs. Anticipating price to fluctuate within \~0.6%. You can earn fees even if the price goes up by 0.3% or goes down by 0.3%.

**Super stable:** Suitable for stable pairs. Anticipating price to fluctuate within \~0.3%. You can earn fees even if the price goes up by 0.15% or goes down by 0.15%.

</details>

### **Step 5**: Specify liquidity amount

Specify the deposit amounts, or how much liquidity you would like to add to open this position. You can either manually type in amounts or use the “Max” and “Half” buttons. Once you specify the deposit amount for one leg of the pair, the corresponding leg’s amount will be automatically calculated and populated for you.

Note: The proportion of liquidity deposited for each leg of the pair is determined by your price range, so it is helpful to set the price range before specifying your deposit amounts.

![Specify deposit amount](https://support.kyberswap.com/hc/article\_attachments/14196998442905)

### **Step 6**: Authorize contract

If you haven’t already done so, you will need to need to authorize the KyberSwap smart contract to transact using your tokens on this network. Click the “Approve \[Token]” button to do so. This will open the approval dialog window on your wallet.

![Approve USDC](https://support.kyberswap.com/hc/article\_attachments/14197014902937)

Once the approval is confirmed, the previously-greyed-out “Preview” button will be clickable.

### **Step 7**: Review liquidity provision transaction

Click on the “Preview” button to bring up the preview screen. Once you have reviewed the information on this screen, click on the “Supply” button to proceed.

![Add liquidity preview for confirmation](https://support.kyberswap.com/hc/article\_attachments/14197015056153)

You will need to confirm this transaction in your wallet.

![Metamask confirmation](https://support.kyberswap.com/hc/article\_attachments/14196998740249)

Once you’ve confirmed the transaction you will see a screen informing you that the transaction has been submitted. You can click on “View Transaction” to view your transaction on the appropriate blockchain explorer.

![Transaction submitted](https://support.kyberswap.com/hc/article\_attachments/14196998903961)

Your new position should now be visible on the My Pools page on KyberSwap.

![Elastic pools dashboard](https://support.kyberswap.com/hc/article\_attachments/14196998929817)
