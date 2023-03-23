---
description: Your KyberSwap Limit Order Questions Answered
---

# FAQ

## Ecosystem

<details>

<summary>Which chains are supported by Limit Orders?</summary>

Limit Orders are a new feature that we are gradually releasing to various chains. It is currently available for use in token swaps on the following chains:

* Ethereum
* BNB Chain
* Polygon
* Avalanche
* Arbitrum
* Optimism
* Fantom

Please refer to [Supported Exchanges and Networks](../../getting-started/supported-exchanges-and-networks.md) for further details.

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

Still can't find what you're looking for? Check out the [KyberSwap Help Center](https://support.kyberswap.com/hc/en-us).
