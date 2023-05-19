---
description: Create An Amplified Pool With Custom Fee Settings
---

# Classic Pool Creation

## Introduction

In order to participate in a **KyberSwap Classic** pool and earn fees, you first need to add liquidity to the pool. You can add liquidity either to an existing pool, or as part of creating a new pool. This guide describes the steps required to **create a new pool by adding liquidity**.

<details>

<summary>Liquidity Provider Flow</summary>

Still deciding on which solution suits you best?&#x20;

* **Overview**: [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
* **Detailed comparison**:  [Classic vs Elastic](../../classic-vs-elastic/)&#x20;

#### Next steps

1. [Connect Your Wallet](../../../kyberswap-solutions/kyberswap-interface/user-guides/connect-your-wallet.md)
2. [Switching Networks](../../../kyberswap-solutions/kyberswap-interface/user-guides/selecting-preferred-network.md)
3. **Classic Pool Creation <-**
4. [Add Liquidity To An Existing Classic Pool](add-liquidity-to-an-existing-classic-pool.md)
5. [Yield Farming On Classic](yield-farming-on-classic.md)
6. [Removing Liquidity On Classic](removing-liquidity-on-classic.md)

</details>

## Adding liquidity to create a new pool

### Step 1: Create a pool

Ensure you are on the correct network, and then click the “Create Pool” button at the top right of the screen.

<figure><img src="../../../.gitbook/assets/image (42).png" alt=""><figcaption><p>Classic Pool page</p></figcaption></figure>

This will bring up the Create a new pool screen, but it will be fairly empty until the parameters of the pool are properly specified.

<figure><img src="../../../.gitbook/assets/image (22) (2).png" alt=""><figcaption><p>Pool creation screen</p></figcaption></figure>

### **Step 2**: Select tokens to add

Select the pair of tokens you would like to create the pool with. You can choose from already whitelisted tokens or [import any token](../../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md) on your chosen network.

<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption><p>Select token pair</p></figcaption></figure>

### Step 3: Enter token amounts

Specify the token amounts to contribute as liquidity to the new pool. Upon entering the two token amounts, the price ratio of the tokens are also displayed at the bottom left of the screen.

Do note that KyberSwap Classic enables users to configure their pool according to their preferred price ranges hence LPs are able to define the starting price of their pool.

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption><p>Token amounts and price ratio</p></figcaption></figure>

{% hint style="danger" %}
#### Price deviations

As a safety precaution, KyberSwap Classic will prompt the LP if the specified pool price deviates significantly from the market price.This is because any liquidity additions that significantly deviates from the market price would immediately result in [impermanent loss](../../../getting-started/foundational-topics/decentralized-finance/impermanent-loss.md) as arbitrageurs sweep up the significantly discounted token from the position.

![](<../../../.gitbook/assets/image (22) (1).png>)
{% endhint %}

### Step 4: Select AMP value

Upon selecting a price ratio, you will then be prompted to enter an AMP value. AMP refers to the amplification factor which enables Classic pools to be siginificantly more capital efficient when it comes to generating yields. By specifying an AMP greater than 1, notice that the active price range also changes accordingly. You will earn any market making fees for trades that happen within this price range but your position will become inactive if trades happen outside this interval.

Please refer to [Amplification Factor](../concepts/dynamic-pricing-curves.md#amplification-factor-amp) for further details on selecting an AMP value.

<figure><img src="../../../.gitbook/assets/image (61).png" alt=""><figcaption><p>Select AMP and corresponding price range</p></figcaption></figure>

### Step 5: Select fee tier

You will then be required to select your fee tier.

<figure><img src="../../../.gitbook/assets/image (68).png" alt=""><figcaption><p>Select fee tier</p></figcaption></figure>

KyberSwap currently offers the following tiers to cater for different token pair correlations:

<details>

<summary><strong>Fee tier options</strong></summary>

1. **0.008% fee tier: Best for very stable pairs**\
   The 0.008% fee tier is ideal for token pairs that typically trade at a fixed or extremely high correlated rate, such as pairs of stablecoins (e.g. DAI-USDC). Liquidity providers take on minimal price risk in these pools, and traders expect to pay minimal fees.
2. **0.01% fee tier: Best for very stable pairs**\
   The 0.01% fee tier is ideal for token pairs that typically trade at a fixed or extremely high correlated rate, such as pairs of stablecoins (e.g. DAI-USDC). Liquidity providers take on minimal price risk in these pools, and traders expect to pay minimal fees.
3. **0.05% fee tier: Best for stable pairs**\
   The 0.04% fee tier is ideal for token pairs that typically trade at a fixed or highly correlated rate, such as pairs of stablecoins (e.g. DAI-USDC). Liquidity providers take on minimal price risk in these pools, and traders expect to pay minimal fees.
4. **0.3% fee tier: Best for most pairs**\
   The 0.30% fee tier is best suited for less correlated token pairs such as the ETH-DAI token pair, which are subject to significant price movements to either upside or downside. This higher fee is more likely to compensate liquidity providers for the greater price risk that they take on relative to stablecoin LPs.
5. **0.5% fee tier: Best for weakly correlated pairs**\
   The 0.5% fee tier is best suited for weakly correlated token pairs such as the ETH-LINK token pair, which are subject to price movements to either upside or downside. This higher fee is more likely to compensate liquidity providers for the greater price risk that they take on relative to stablecoin liquidity providers.
6. **1% fee tier: Best for exotic pairs**\
   The 1% fee tier is best suited for even less correlated token pairs such as the ETH-KNC token pair, which are subject to significant price movements to either upside or downside. This higher fee is more likely to compensate liquidity providers for the greater price risk that they take on relative to stablecoin liquidity providers.

</details>

### **Step 6**: Authorize contract

If you haven’t already done so, you will need to need to authorize the KyberSwap smart contract to transact using your tokens on this network. Click the “Approve \[Token]” button to do so. This will open the approval dialog window on your wallet.

<figure><img src="../../../.gitbook/assets/image (56).png" alt=""><figcaption><p>Approve KNC</p></figcaption></figure>

### Step 7: Review pool creation

Click on the "Create" button to bring up the preview screen. Once you have reviewed the information on this screen, click on the "Create Pool" button to proceed.

<figure><img src="../../../.gitbook/assets/image (15) (2).png" alt=""><figcaption><p>Create pool preview</p></figcaption></figure>

You will need to confirm this transaction in your wallet

<figure><img src="../../../.gitbook/assets/image (35).png" alt=""><figcaption><p>KyberSwap pending confirmation from wallet</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (6) (2).png" alt=""><figcaption><p>Metamask confirmation</p></figcaption></figure>

Once you’ve confirmed the transaction you will see a screen informing you that the transaction has been submitted. You can click on “View Transaction” to view your transaction on the appropriate blockchain explorer.

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption><p>Transaction submitted</p></figcaption></figure>

Your new position should now be visible on the My Pools page on KyberSwap.

<figure><img src="../../../.gitbook/assets/image (48).png" alt=""><figcaption><p>My Pools - Classic Pools </p></figcaption></figure>
