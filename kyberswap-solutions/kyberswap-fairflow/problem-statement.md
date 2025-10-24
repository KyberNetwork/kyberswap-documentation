# Problem Statement

In traditional AMM models, LPs provide liquidity to earn LP fees (gain side) as compensation for Impermanent Loss (loss side). When prices revert to their original level to make Impermanent Loss equal zero, it may appear that LPs haven't lost anything. However, in reality, LPs still incur Opportunity Value Loss, which is captured by arbitrage activity.

To simplify the concept, we have a basic example here (some technical details have been omitted): Imagine you provide full-range liquidity with 1 ETH + 1,000 USDC when ETH is priced at $1,000.

* When ETH price increases to $2,000, your LP position rebalances to \~0.707 ETH and 1,414 USDC which is equivalent to selling \~0.293 ETH for 414 USDC. However, if you kept your ETH and sold it now, you would have received 586 USDC.
* The $172 difference (586 USDC - 414 USDC) represents Impermanent Loss. It also reflects the Opportunity Value Loss from arbitrage in a simple case where the pool doesn’t rebalance automatically, the LP can withdraw 0.293 ETH by adding 414 USDC (to rebalance the pool) and sell these ETH elsewhere for 586 USDC.
* Later, when ETH returns to $1,000, your LP position reverts to 1 ETH and 1,000 USDC. Following the same logic, it's as if you used 414 USDC to buy back \~0.293 ETH. However, you could have repurchased \~0.293 ETH for just 293 USDC. This results in an additional Opportunity Value Loss of $121.
* At the endpoint (when ETH returns to $1,000), the LP incurs an $293 ($172+$121) in Opportunity Value Loss\* from arbitrage activity in a simple case - even though the Impermanent Loss is zero.

\*_In reality, the Opportunity Value Loss from arbitrage can be greater than in the simplified example, because prices typically do not move directly from $1,000 to $2,000 and back. Instead, they fluctuate intensively in between, creating more opportunities for arbitrage activities._

_Note: This simplified example is for conceptual illustration only. The figures are not based on any simulation. Refer to the table below for actual simulation results._

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

