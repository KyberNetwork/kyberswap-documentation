# FAQs

#### **Will I always get exactly my trigger price?**

The trigger price decides _when_ the order is executed, not the price it is executed at. **Min. Receive** — your trigger price, less your maximum slippage, less the fee — is the least you can receive, and it is shown on the review screen before you sign. See [What decides where an order is executed?](./#what-decides-where-an-order-is-executed).



#### **If my token has low liquidity when the trigger price is reached, will the swap still go through?**

Only if it can return at least your Min. Receive. When liquidity is thin the swap returns less, and if that falls below Min. Receive the order shows as **Retrying** with your tokens still in your wallet. The order row names the cause and offers **Edit order** where your maximum slippage is what is blocking it — see [The trigger price was reached, but my order has not been completed](manage-stop-market-orders.md#the-trigger-price-was-reached-but-my-order-has-not-completed).



#### **What happens if the Oracle feed for my token is deprecated or out of date?**

An order is executed only while the Oracle feed for its token is valid. Two cases stop execution:

* **The feed is deprecated or flagged as unsafe.** If Chainlink deprecates the price feed for a token, or flags it as unsafe, orders on that token are not executed.
* **The latest price is out of date.** Each token’s feed has its own heartbeat — the longest time allowed between updates, for example, one hour. If the latest Oracle price is older than that, it is treated as stale, and the order is not executed until the feed updates.

In both cases, nothing is swapped, and the tokens stay in your wallet.



#### **Can a Stop Market be triggered by a manipulated price?**

The trigger is evaluated against an Oracle price, powered by Chainlink, which is aggregated from many sources rather than from a single liquidity pool - see [Which price does a Stop Market monitor?](./#which-price-does-a-stop-market-monitor)



#### **What happens during very high network gas?**

The order waits. It stays in your Active Orders showing **Retrying**, your tokens stay in your wallet, and it is attempted again once gas settles.

The fee covers the on-chain execution cost, so attempts pause while gas would take up more than **90%** of it, or runs far above its recent baseline. Small orders wait most often, because their fee covers less gas — see [When the fee is a large share of a small order](../../getting-started/fee-schedule.md#when-the-fee-is-a-large-share-of-a-small-order).



#### **My order triggered but has not completed. Where are my tokens?**

In your wallet. Nothing moves unless the swap completes. The order is in **Retrying** — see[ The trigger price was reached, but my order has not been completed](manage-stop-market-orders.md#the-trigger-price-was-reached-but-my-order-has-not-completed).





#### **Can I place more than one Stop Market order on the same token?**

Yes, as long as their combined amounts stay within your wallet balance — with 2 ETH you could place two orders of 1 ETH, but not two of 2 ETH. To free up the amount, cancel an order or edit it to free up balance. See [What happens if your balance changes?](./#what-happens-if-your-balance-changes).
