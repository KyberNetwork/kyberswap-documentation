---
description: Manage Your Positions Effortlessly
---

# Cancel Limit Orders

## Introduction

We understand that DeFi markets are volatile and users need to quickly react to such changes. KyberSwap Limit Orders enables you to cancel your orders at any time. As long as the order is still active (not expired or fully filled), you can easily cancel your order on the KyberSwap Interface.&#x20;

For convenience, KyberSwap offers the option to cancel a single order or all active orders.

## How to cancel a specific limit order

You can manually cancel your order (or any unfilled portion of your order) before it expires.

{% hint style="info" %}
#### Limit Order modification gas fees

Note that limit order cancelation is an on-chain transaction which requires gas fees to be processed. This is because the signed maker transaction is distributed across our network of off-chain takers. As all potential takers now have a copy of the maker transaction, the only way to guarantee cancellation is to send a cancellation transaction to the chain so that if any other takers match and execute the maker transaction on-chain, the limit order will fail.
{% endhint %}

### **Step 1**: Select active order

Find the active order you would like to update and click on its red Cancel button. The button icon looks like a trash can. This will bring up the Cancel Order screen.

![Cancel order](https://support.kyberswap.com/hc/article\_attachments/14668245051673)

### **Step 2**: Review cancellation

Review the information presented on the Cancel Order screen then click “Cancel” once you are satisfied. This is an [on-chain transaction](../concepts/off-chain-relay.md) that will require approval and gas.

![Confirm cancellation](https://support.kyberswap.com/hc/article\_attachments/14668245165337)

Once the cancel transaction is confirmed on the blockchain, the cancelled order will appear under your Cancelled Orders in your Order History.

## How to cancel all active limit orders

You can also cancel all active orders as long as they are completely or partially unfilled.

### **Step 1**: Select cancel all

Click on the red “Cancel All” button. This will bring up a Cancel Order screen.

![Cancel all orders](https://support.kyberswap.com/hc/article\_attachments/14668230007065)

### **Step 2**: Confirm cancellation

Click “Cancel” to confirm the Cancel All action. This is an [on-chain transaction](../concepts/off-chain-relay.md) that will require approval and gas.

![Confirm cancellation of all orders](https://support.kyberswap.com/hc/article\_attachments/14668245165337)

Any limit orders cancelled in this manner will appear under your Cancelled Orders in your Order History.
