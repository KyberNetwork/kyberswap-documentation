---
description: Easily Transfer Tokens From One Chain To Another
---

# Bridge Your Assets Across Multiple Chains

## Introduction

KyberSwap has integrated the Multichain cross-chain router protocol to enable our customers to quickly bridge coins between different networks directly on [https://kyberswap.com/bridge](https://kyberswap.com/bridge).

More information can be found on our third-party integration [page](../../../reference/third-party-integrations.md).

<figure><img src="../../../.gitbook/assets/Kyber Multichain.png" alt=""><figcaption><p>KyberSwap x Multichain</p></figcaption></figure>

<details>

<summary>Trader Flow</summary>

1. [Connect Your Wallet ](connect-your-wallet.md)
2. [Switching Networks ](selecting-preferred-network.md)
3. Get Tokens
   * [Get Crypto With Fiat](get-crypto-with-fiat.md)&#x20;
   * **Bridge Your Assets Across Multiple Chains** **<-**
4. Swap Tokens
   * [Instantly Swap At The Best Rates ](instantly-swap-at-the-best-rates.md)
   * [Swap At Your Preferred Rates ](trade-at-your-preferred-rates.md)

</details>

<details>

<summary>Disclaimer on use of Third-party Integration/Service</summary>

For ease of communication, KyberSwap is referred to as "we" in this disclaimer. Any natural persons or other entities who engages in any activities on KyberSwap shall be considered as the user of KyberSwap, and is referred to as "you" in the disclaimer. We hereby remind you of the risks involved in using third-party services (referred to herein as “third-party services”).

1. Your use of any third-party services on KyberSwap is your personal decision and we have no control over it.
2. We are not responsible for the audit of any third-party services, nor do we make any commitments or guarantees on the validity, accuracy, correctness, reliability, quality, stability, completeness and/or timeliness of the technology and information involved in such third-party services and their associated services.
3. You are solely responsible for all outcomes arising from your choice to use the third-party services and their associated services.
4. You shall make your own judgement and evaluation as to whether any third-party services and its associated services comply with the applicable laws, regulations and relevant policy requirements of your jurisdiction. We do not provide any recommendation and opinions on this subject apart from recommending you to strictly abide by the laws and regulations of your jurisdiction.
5. Outcomes and occurrences which arise out of your use of any third-party services, including but not limited to legal issues, contract liability issues, and economic loss issues, shall be resolved between you and the relevant third-party services. We are not responsible for the resolution of any outcomes or disputes arising from your choice to use the third-party services.
6. We will not share any information with any third-party services unless under your consent. Once we receive your consent, you shall be solely responsible for all legal liabilities and disputes resulting from any third-party services access to your personal information and such labilities and disputes shall be resolved between you and the relevant third-party services.

**Our provision of access to third-party services on KyberSwap does not amount to any kind of recommendation, endorsement, or advice to use any third-party services or its associated services.**

</details>

## Multichain

Multichain is the ultimate Router for web3. It is an infrastructure developed for arbitrary cross-chain interactions.

* It enables assets transfers between any two or more chains.
* It can work with pre-existing assets on blockchains, by using liquidity pools for those assets.
* It can also work with Bridged assets smart contract, where Multichain is responsible for minting assets on chains. This allows a generalisation of Bridges, so that assets are not restricted to having to return to their source chain before being sent to another chain. This makes for a cost effective solution for users, especially if the asset originated on Ethereum.
* The Router can include both native and Bridged assets. This allows inclusion of assets that might have been generated with a third party bridge (though we would need to understand what bridges were originally used).

Click [**here**](https://docs.multichain.org/getting-started/introduction) for more information on Multichain Bridge.

## KyberSwap Integration:

Multichain is integrated on KyberSwap through API front end functionality to provide users with an option to easily bridge tokens across chains.

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption><p>Bridge assets across chains on KyberSwap with Multichain</p></figcaption></figure>

Click [**here**](https://docs.multichain.org/getting-started/introduction)[ ](https://blog.kyber.network/kyberswap-launches-multichain-integration-39e12c42fb73)for the official announcement.

## Bridge your token from one chain to the next

### **Step 1**: Navigate to the bridge interface

The link to the bridge interface can be found within the "Swap" dropdown of the KyberSwap landing page. Alternatively, you can go directly to [https://kyberswap.com/bridge](https://kyberswap.com/bridge).

<figure><img src="../../../.gitbook/assets/image (16) (1) (1).png" alt=""><figcaption><p>Bridge navigation</p></figcaption></figure>

### **Step 2**: Select token and chains

Select the token you’d like to bridge as well as the origin and destination networks.

![Transfer token from BSC to Polygon](https://support.kyberswap.com/hc/article\_attachments/14001341138969)

### **Step 3**: Configure bridging route

Select the token pool you would like to use for the bridge. Different pools may have different liquidity and fees.

![Select route](https://support.kyberswap.com/hc/article\_attachments/14001360263577)

### **Step 4**: Approve smart contract token allowance

Click the “Approve \[token]” button to authorize the Multichain smart contract to use your wallet’s balance. There is a network fee associated with this transaction, but this only needs to be done once per token.

![Approve multichain contract](https://support.kyberswap.com/hc/article\_attachments/14001341345049)

### **Step 5**: Review transaction details

If Multichain is approved, you should see a “Review Transfer” button. Click on that to proceed. The transfer details should appear.

![Review transfer](https://support.kyberswap.com/hc/article\_attachments/14001360470041)

### **Step 6**: Confirm the transaction

Once you have reviewed and are satisfied with the details, click on the “Transfer” button to initiate the transaction. You will be prompted by your wallet to approve or confirm the transaction.

![Metamask approval](https://support.kyberswap.com/hc/article\_attachments/14001360628633)

Once you’ve confirmed the transaction you will see a screen informing you that the transaction has been submitted. You can click on “View Transaction” to view your transaction on the appropriate blockchain explorer.

![Transaction submitted](https://support.kyberswap.com/hc/article\_attachments/14001360648473)

You should also see the transaction listed in your Transfer History.

![Transfer history](https://support.kyberswap.com/hc/article\_attachments/14001485321241)
