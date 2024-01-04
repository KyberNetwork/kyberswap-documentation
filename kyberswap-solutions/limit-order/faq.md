---
description: Your KyberSwap Limit Order Questions Answered
---

# FAQ

## General

<details>

<summary>Which chains are supported by Limit Orders?</summary>

The full list of supported chains can be found on [Supported Exchanges and Networks](../../getting-started/supported-exchanges-and-networks.md).

</details>

<details>

<summary>Which tokens does Limit Orders support?</summary>

KyberSwap whitelists well-known tokens for ease of access, but you can import custom tokens that meet the ERC20 standard via our user interface. For more information on how to do this, please refer to [Add Your Favourite Tokens](../kyberswap-interface/user-guides/add-your-favourite-tokens.md).

</details>

## Trading

<details>

<summary>How do I tell If my Limit Order has been filled?</summary>

Under your Active Orders, you should be able to see a yellow progress bar if your order has been partially filled. You can click on the dropdown button next to the order to see the individual taker orders that partially filled your limit order.

<img src="https://support.kyberswap.com/hc/article_attachments/14668248790041" alt="001_FilledProgress.png" data-size="original">

If you cannot find your order on the Active Orders tab, it may have been completely filled. Filled limit orders appear under your Order History and have a full green progress bar. You can click on the dropdown button next to the order to see the individual taker orders that contributed to filling your limit order.

<img src="https://support.kyberswap.com/hc/article_attachments/14668248798489" alt="002_100PercentFilledGreen.png" data-size="original">

</details>

<details>

<summary>Why is my Limit Order not being filled?</summary>

Here are a few common reasons for Limit Orders not being filled.

#### The exact limit order price target might not have been reached.

There might be a difference in the the price of your limit order and the current market price. The chance of your order being filled increases as the market price gets closer to your order’s price.

#### The order might not have been profitable for a taker.

Takers must consider the order's size, gas fees, and personal profit margin before deciding to fill your order. Furthermore, some takers might only fill part of your limit order, and then seek out more profitable orders elsewhere.

#### The order involves tokens that have low trading volumes.

Orders that involve exotic tokens or token pairs may have fewer takers to fill the order.

</details>

<details>

<summary>Why can't I view my order?</summary>

There are several factors that can make you not see your order:

* The transactions might not have been signed before placing
* The order was already executed (you can check in Order History tab)
* The page needs to be refreshed.

</details>

<details>

<summary>Why does modifying or canceling my limit order incur gas fees?</summary>

You can now cancel for free with [gasless cancel](concepts/gasless-cancellation.md). Please refer to [Cancellation Options ](user-guides/cancel-limit-orders.md#cancellation-options)for the user guide.

For users who require cancellation to be instant, KyberSwap provides a [hard cancel](concepts/gasless-cancellation.md#hard-cancel) option. Gas is required in this case as the signed maker transaction (i.e. newly created order)  is distributed to our network of off-chain takers. As all potential takers now have a copy of the maker transaction, the only way to guarantee cancellation is to send a cancellation transaction to the chain so that if any other takers match and execute the maker transaction on-chain, the limit order will fail.

Please refer to [Off-Chain Relay, On-Chain Settlement](concepts/off-chain-relay.md) for further details on the Limit Order mechanism.

</details>

Still can't find what you're looking for? Check out the [KyberSwap Help Center](https://support.kyberswap.com/hc/en-us).
