---
description: Your KyberSwap Limit Order Questions Answered
---

# FAQ

## General

#### Which chains are supported by Limit Orders?

The full list of supported chains can be found on [Supported Exchanges and Networks](../../getting-started/supported-exchanges-and-networks.md).



#### Which tokens does Limit Orders support?

KyberSwap whitelists well-known tokens for ease of access, but you can import custom tokens that meet the ERC20 standard via our user interface. For more information on how to do this, please refer to [Add Your Favourite Tokens](../user-guides/add-your-favourite-tokens.md).

## Trading

#### How do I tell If my Limit Order has been filled?

Under your Active Orders, you should be able to see a yellow progress bar if your order has been partially filled. You can click on the dropdown button next to the order to see the individual taker orders that partially filled your limit order.

<img src="https://support.kyberswap.com/hc/article_attachments/14668248790041" alt="001_FilledProgress.png" data-size="original">

If you cannot find your order on the Active Orders tab, it may have been completely filled. Filled limit orders appear under your Order History and have a full green progress bar. You can click on the dropdown button next to the order to see the individual taker orders that contributed to filling your limit order.

<img src="https://support.kyberswap.com/hc/article_attachments/14668248798489" alt="002_100PercentFilledGreen.png" data-size="original">



#### Why is my Limit Order not being filled?

Here are a few common reasons for Limit Orders not being filled.

**The exact limit order price target might not have been reached.**

There might be a difference in the the price of your limit order and the current market price. The chance of your order being filled increases as the market price gets closer to your order’s price.

**The order might not have been profitable for a taker.**

Takers must consider the order's size, gas fees, and personal profit margin before deciding to fill your order. Furthermore, some takers might only fill part of your limit order, and then seek out more profitable orders elsewhere.

**The order involves tokens that have low trading volumes.**

Orders that involve exotic tokens or token pairs may have fewer takers to fill the order.



#### Why can't I view my order?

There are several factors that can make you not see your order:

* The transactions might not have been signed before placing
* The order was already executed (you can check in Order History tab)
* The page needs to be refreshed.



#### Why does modifying or canceling my limit order incur gas fees?

You can now cancel for free with [gasless cancel](../../kyberswap-solutions/limit-order/concepts/gasless-cancellation.md). Please refer to [Cancellation Options ](cancel-limit-orders.md#cancellation-options)for the user guide.

For users who require cancellation to be instant, KyberSwap provides a [hard cancel](../../kyberswap-solutions/limit-order/concepts/gasless-cancellation.md#hard-cancel) option. Gas is required in this case as the signed maker transaction (i.e. newly created order) is distributed to our network of off-chain takers. As all potential takers now have a copy of the maker transaction, the only way to guarantee cancellation is to send a cancellation transaction to the chain so that if any other takers match and execute the maker transaction on-chain, the limit order will fail.

Please refer to [Off-Chain Relay, On-Chain Settlement](../../kyberswap-solutions/limit-order/concepts/off-chain-relay.md) for further details on the Limit Order mechanism.



#### Why did I receive less value than the market price when my Limit Order was filled?

A Limit Order locks in a **fixed rate** at the time you sign it. When your order is filled, you receive exactly the rate you create - regardless of where the market price is at the time of execution.

For example, if you create an order to sell 1,000 Token A at a rate of 0.50 USDC per token, you will receive 500 USDC when filled - even if Token A's market price has risen to 0.80 USDC by then.

This is how limit orders work:

* **You (the maker)** set a specific rate and sign the order.
* **A taker** fills your order when they find it profitable to do so — typically when the market price has reached or moved above your specified rate.
* **You receive** exactly the amount defined by your order. The taker acquires your tokens at your rate and may sell them at the prevailing market price.

If the market price rises significantly after you place your order, your order still fills at the original rate you set. To avoid this, you can **cancel and re-create** your order at an updated rate. Gasless cancellation is available - see [Cancel a Limit Order](cancel-limit-orders.md) for details.
