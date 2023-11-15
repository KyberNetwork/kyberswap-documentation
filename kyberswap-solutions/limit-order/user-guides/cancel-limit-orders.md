---
description: Manage Your Positions Effortlessly
---

# Cancel Limit Orders

## Introduction

We understand that DeFi markets are volatile and users need to quickly react to such changes. KyberSwap Limit Orders enables you to cancel your orders at any time. As long as the order is still active (not expired or fully filled), you can easily cancel your order on the KyberSwap Interface.&#x20;

For convenience, KyberSwap also offers the option to cancel a single order or all active orders.

## Cancellation options

KyberSwap Limit Order offers 2 modes of cancellation depending on your trading requirements:

* [**Gasless Cancel**](../concepts/gasless-cancellation.md#gasless-cancel): Cancel your limit order without incurring gas fees. Upon triggering gasless cancel, users might need to wait up to 5 minutes for the cancellation to be confirmed.
* [**Hard Cancel**](../concepts/gasless-cancellation.md#hard-cancel): Instantly cancel your limit order by incurring a small prioritization gas fee. Upon triggering hard cancel, users will need to confirm the gas fee whereupon cancellation is confirmed once the transaction has been mined.

{% hint style="info" %}
**Cancellation mechanisms**

Please refer to [Gasless Cancellation](../concepts/gasless-cancellation.md) for an overview of how KyberSwap achieves limit order cancellation both on-chain (i.e. Hard Cancel) and off-chain (i.e. Gasless Cancel).
{% endhint %}

## How to cancel a specific limit order

You can manually cancel your order (or any unfilled portion of your order) before it expires.

### **Step 1**: Select active order

Find the active order you would like to update and click on its red Cancel button. The button icon looks like a trash can. This will bring up the Cancel Order screen:

![Cancel order](../../../.gitbook/assets/LO\_Cancellation\_Button.png)

### **Step 2**: Review cancellation

On the cancellation pop-up, you will be provided with 2 options for cancellation:

* [**Gasless Cancel**](../concepts/gasless-cancellation.md#gasless-cancel): Cancel without paying gas. In cases where the LO is close to the market rate, you might need to wait a maximum of 5 minutes.
* [**Hard Cancel**](../concepts/gasless-cancellation.md#hard-cancel): Pay a small prioritization gas fee to immediately cancel your order.

Please refer to our [Gasless Cancellation](../concepts/gasless-cancellation.md) page for more details on how KyberSwap Limit Orders enable trades without gas.

![Confirm cancellation](../../../.gitbook/assets/LO\_Cancellation\_Preview.png)

Review the information presented on the Cancel Order screen and select your cancellation option. You can then proceed by clicking the "Cancel Order" once you are satisfied.

{% tabs %}
{% tab title="Gasless Cancel" %}
This is an [off-chain](../../../getting-started/foundational-topics/decentralized-technologies/on-chain-vs-off-chain-data.md) transaction which requires another signature and is almost immediate in most cases. If your order was recently included in a taker or aggregator quote, a countdown timer will be shown indicating the waiting time (maximum 5 mins) until your order is gaslessly cancelled.

Once the cancellation is confirmed by the KyberSwap Operator, the cancelled order will appear under your Cancelled Orders in your Order History.
{% endtab %}

{% tab title="Hard Cancel" %}
This is an [on-chain transaction](../concepts/off-chain-relay.md) that will require approval and gas fees to be paid to the network.

Once the cancel transaction is confirmed on the blockchain, the cancelled order will appear under your Cancelled Orders in your Order History.
{% endtab %}
{% endtabs %}

## How to cancel all active limit orders

You can also cancel all active orders as long as they are completely or partially unfilled.

### **Step 1**: Select cancel all

Click on the red “Cancel All” button. This will bring up a Cancel Order screen.

![Cancel all orders](<../../../.gitbook/assets/LO\_CancellationBulk\_Button (2).png>)

### **Step 2**: Confirm cancellation

Select your cancellation option and click “Cancel” to confirm the Cancel All action. Refer [Review Cancellation](cancel-limit-orders.md#step-2-review-cancellation) in the section above for details regarding the options.

![Confirm cancellation of all orders](../../../.gitbook/assets/LO\_CancellationBulk\_Preview.png)

Any limit orders cancelled in this manner will appear under your Cancelled Orders in your Order History.
