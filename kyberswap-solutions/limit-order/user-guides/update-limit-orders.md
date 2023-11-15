---
description: Manage Your Positions Effortlessly
---

# Update Limit Orders

## Introduction

We understand that DeFi markets are volatile and users need to quickly react to such changes. As such, KyberSwap Limit Orders enables you to modify your orders at any time. As long as the order is still active (not expired or fully filled), you can easily modify your order on the KyberSwap Interface.&#x20;

## How to update a limit order

If you have an open order that you would like to amend, you can update it through the Active Orders interface, but please note that this functionally is the same as performing the following two steps combined into a single transaction:

* Canceling the open order
* Creating a new open order with new parameters

{% hint style="info" %}
#### Limit Order modification gas fees

Note that limit order update is an on-chain transaction which requires gas fees to be processed. This is because the signed maker transaction is distributed across our network of off-chain takers. As all potential takers now have a copy of the maker transaction, the only way to guarantee cancellation is to send a cancellation transaction to the chain so that if any other takers match and execute the maker transaction on-chain, the limit order will fail.
{% endhint %}

### **Step 1**: Select active order

Find the active order you would like to update and click on its green Edit button. The button icon looks like a pen. This will bring up the Edit Order screen:

![Edit active order](../../../.gitbook/assets/LO\_Edit\_Button.png)

### **Step 2**: Modify the order parameters

Amend the parameters of your limit order in the Edit Order screen. You can change one or more of the following parameters:

* The amount of token being offered (”You Sell”)
* The price (”Sell \[token] at rate”)
* The time limit (”Expires In”)
* The edit option (See [Gasless Cancellation](../concepts/gasless-cancellation.md) for more info)

You cannot amend the token swap pair.

![Edit order pop-up](../../../.gitbook/assets/LO\_Edit\_Preview.png)

Click on “Edit Order” to proceed.

### **Step 3**: Review your modified order

Review the details of the order in the “Review your order” screen that appears. Once you are satisfied, click on the “Place Order” button.&#x20;

* If you chose the "Gasless Edit" option, this will be an [off-chain transaction](../../../getting-started/foundational-topics/decentralized-technologies/on-chain-vs-off-chain-data.md) which requires 2 signatures for cancellation and creating a new order.
* If you chose the "Hard Edit" option, this will be an [on-chain transaction](../concepts/off-chain-relay.md) that requires an approval and gas.

![Review order](../../../.gitbook/assets/LO\_Edit\_Confirmation.png)

The new limit order with updated parameters should now appear on your Active Orders list, and the old limit order will now be listed under your Cancelled Orders in your Order History.
