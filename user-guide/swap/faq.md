---
description: Your KyberSwap Aggregator Questions Answered
---

# FAQ

## General

**Which chains does KyberSwap Aggregator support?**

The full list of supported chains can be found on [Supported Exchanges and Networks](../../getting-started/supported-exchanges-and-networks.md).

**Which tokens does KyberSwap Aggregator support?**

KyberSwap whitelists well-known tokens for ease of access, but you can import custom tokens that meet the ERC20 standard via our user interface. For more information on how to do this, please refer to [Add Your Favourite Tokens](../user-guides/add-your-favourite-tokens.md).

**How does KyberSwap find the best swap rate?**

KyberSwap uses [Dynamic Trade Routing](../../developer-guide/start-here/foundational-solutions/dynamic-trade-routing.md) to split and route trades across capital-efficient liquidity sources at quote time. In addition, [Smart Settlement](../../developer-guide/start-here/foundational-solutions/smart-settlement-better-swap-output-with-lower-slippage.md) compares candidate pools on-chain at execution time and selects the one that delivers the highest token output. Together, these mechanisms ensure that you receive optimal rates at quote time and verified execution at swap time.

**Do I need to create an account to swap on KyberSwap?**

No. KyberSwap is a fully non-custodial, permissionless protocol. You only need a Web3 wallet (such as MetaMask, Rabby, or WalletConnect-compatible wallets) to connect and swap. No registration, email, or KYC is required.

**What is Smart Settlement?**

Smart Settlement is an upgrade to KyberSwap's swap execution that compares multiple candidate pools on-chain at the moment your transaction executes — and selects the one that delivers the highest token output. It works automatically on top of Dynamic Trade Routing with no additional fees or user configuration. For full details, see [Smart Settlement](../../developer-guide/start-here/foundational-solutions/smart-settlement-better-swap-output-with-lower-slippage.md).



## Trading

**What is slippage and how does it affect my swap?**

Slippage is the difference between the quoted swap rate and the rate you actually receive when the transaction executes. It occurs because market conditions can change between the time you request a quote and the time your transaction is processed on-chain. KyberSwap allows you to set a slippage tolerance — if the actual rate falls below this threshold, the transaction will revert to protect you. For more details, see [Slippage](../../getting-started/foundational-topics/decentralized-finance/slippage.md).

**How do I change slippage tolerance?**

Slippage tolerance for swaps defaults to different values depending on the token pair's categorization, but you can change this in Swap settings.

For more information on completing a swap, you can refer to [Instantly Swap At The Best Rates](./) for a step-by-step guide.

**What is price impact?**

Price impact is the effect your trade has on the market price of a token within a liquidity pool. Larger trades relative to the pool's liquidity depth will move the price more, resulting in a less favorable rate. KyberSwap's Dynamic Trade Routing minimizes price impact by splitting trades across multiple pools and liquidity sources. For more details, see [Price Impact](../../getting-started/foundational-topics/decentralized-finance/price-impact.md).

**Can I swap any ERC-20 token on KyberSwap?**

KyberSwap supports swapping any standard ERC-20 token that has liquidity on the integrated DEXs for the connected chain. Whitelisted tokens are displayed by default, but you can import custom tokens by pasting the token contract address. Note that some tokens implement fee-on-transfer (FOT) mechanisms where a percentage of tokens is burned or redistributed on each transfer — KyberSwap supports these tokens but the output amount will reflect the fee deduction. Always verify token contract addresses before importing custom tokens.

**What is the minimum or maximum swap amount?**

There is no minimum or maximum swap amount enforced by KyberSwap. However, very small swaps may not be economical due to network gas fees, and very large swaps may experience higher price impact depending on available liquidity. KyberSwap's route display will show the estimated output and price impact before you confirm the swap.

**How do I swap between different chains?**

To swap tokens across different blockchain networks, use KyberSwap's [Cross-chain Swap](../cross-chain-swap.md) feature, which integrates with third-party bridge providers to find optimal routes and rates for cross-chain transactions. For single-chain swaps, simply connect your wallet and select the desired network using the chain selector on the swap page.



## Security & Protection

**How does KyberSwap protect me against MEV and sandwich attacks?**

KyberSwap provides multiple layers of protection. Your slippage tolerance setting ensures the transaction reverts if the rate moves beyond your threshold. [Smart Settlement](../../developer-guide/start-here/foundational-solutions/smart-settlement-better-swap-output-with-lower-slippage.md) adds an additional layer of resilience: if your selected pool is sandwiched or front-run within the same block, Smart Settlement can detect the worsened rate and switch to an unaffected pool with better output. For more on MEV, see [Maximal Extractable Value (MEV)](../../getting-started/foundational-topics/decentralized-finance/maximal-extractable-value-mev.md).



## Troubleshooting

**Why is my transaction stuck in "Pending" state?**

*   Reasons for stuck transactions

    If your swap transaction was successfully accepted by the KyberSwap platform but you see on your transaction history and on blockchain explorers that the transaction has been stuck in a “pending” state for more than a few blocks, this could be due to one of several reasons:

    * Low Gas Limit: During periods of high network activity, gas prices tend to increase. If you’ve set your Web3 wallet to use a gas limit that is relatively low, it may take some time before miners pick up your transaction from the mempool.
    * Multiple Transactions Held Up by One Slow Transaction: If you have sent several transactions within a short amount of time, some of your transactions could be held up behind one or more transactions that are pending due to low gas limits.
*   How to fix stalled transactions

    If the transaction is stalled (stuck in a pending state) in the mempool and has zero block confirmations, you can either cancel it or expedite it be rebroadcasting the transaction using the same nonce as the pending transaction. This action will incur its own network fee and is performed through your Web3 wallet software.

    If you have a queue of stuck transactions, you may only need to cancel/expedite the first few transactions before the rest get unstuck on their own.

    Here are links to instructions on how to perform this action on some of the more common Web3 wallets.

    * [Metamask](https://support.metamask.io/manage-crypto/transactions/how-to-speed-up-or-cancel-a-pending-transaction/)
    * [Trust Wallet](https://support.trustwallet.com/support/solutions/articles/67000635278-why-is-my-transaction-pending-or-stuck-)
    * [MEW](https://help.myetherwallet.com/en/articles/5461454-canceling-or-replacing-a-transaction-after-it-s-been-sent)
    * [1inch iOS Wallet](https://help.1inch.io/en/articles/5211509-how-to-cancel-or-speed-up-a-pending-transaction-in-the-1inch-wallet)
    * [Crypto.com Defi Wallet](https://help.crypto.com/en/articles/4476691-how-do-i-cancel-or-speed-up-my-pending-eth-erc-20-transaction-on-crypto-com-defi-wallet-with-replace-by-fee)

**Why did my swap transaction fail?**

Swap transactions can fail for several reasons: your slippage tolerance was too low and the price moved beyond your threshold before execution; the token's liquidity changed significantly between quoting and execution; the gas limit was insufficient for the transaction; or the token contract has custom logic (such as transfer restrictions or pausing) that prevented the swap. You can try again with a higher slippage tolerance, ensure sufficient gas, or check whether the token has any transfer restrictions.

You can always reach out to KyberSwap’s Customer Support via #create-ticket on Discord server: [https://discord.gg/kyberswap](https://discord.gg/kyberswap).

**I received fewer tokens than expected**

Before confirming a swap transaction, you will be shown an order confirmation screen that clearly displays the tokens you will receive after the swap. This screen helps to ensure that there are no unpleasant surprises; you will never receive fewer tokens than the minimum amount displayed on this screen if the swap is successful.

Do pay particular attention to the [Price Impact](../../getting-started/foundational-topics/decentralized-finance/price-impact.md) and [Slippage](../../getting-started/foundational-topics/decentralized-finance/slippage.md) numbers. For further details, please refer to [Confirm the swap](./#step-5-confirm-the-swap).

<img src="../../.gitbook/assets/image (71).png" alt="" data-size="original">





Still can't find what you're looking for? Reach out to us on [Discord](https://discord.gg/kyberswap).
