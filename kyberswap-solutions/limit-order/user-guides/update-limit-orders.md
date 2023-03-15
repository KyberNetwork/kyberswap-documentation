---
description: Change Your Mind Freely
---

# Update Limit Orders

## Introduction

We understand that DeFi markets are volatile and users need to quickly react to such changes without incurring additional fees. KyberSwap Limit Orders enables you to modify your orders at any time without incurring any gas fees. As long as the order is still active (not expired or fully filled), you can easily modify your order on the KyberSwap Interface.&#x20;

## How to update a limit order

If you have an open order that you would like to amend, you can update it through the Active Orders interface, but please note that this functionally is the same as performing the following two steps combined into a single onchain transaction:

* Canceling the open order
* Creating a new open order with new parameters

### **Step 1**: Select active order

Find the active order you would like to update and click on its green Edit button. The button icon looks like a pen. This will bring up the Edit Order screen.

![Edit active order](https://support.kyberswap.com/hc/article\_attachments/14668227864473)

### **Step 2**: Modify the order parameters

Amend the parameters of your limit order in the Edit Order screen. You can change one or more of the following parameters:

* The amount of token being offered (”You Pay”)
* The price (”Sell \[token] at rate”)
* The time limit (”Expires In”)

You cannot amend the token swap pair.

![Edit order pop-up](https://support.kyberswap.com/hc/article\_attachments/14668227865241)

Click on “Review Order” to proceed.

### **Step 3**: Review your modified order

Review the details of the order in the “Review your order” screen that appears. Once you are satisfied, click on the “Place Order” button. This is an onchain transaction that requires an approval and gas.

![Review order](https://support.kyberswap.com/hc/article\_attachments/14668227961881)

The new limit order with updated parameters should now appear on your Active Orders list, and the old limit order will now be listed under your Cancelled Orders in your Order History.
