# Zap

## Problem: Gas Fees And Capital Efficiency

As a Liquidity Provider, one of the major pain points when contributing liquidity to [AMM pools](automated-market-maker.md) is the  need to source the exact ratio of tokens at the point of adding liquidity. For example, if you are adding liquidity to a USDC-WETH pool but only had 1,000USDC in your wallet, you would have go through multiple steps:

* Check the ratio of tokens required for adding liquidity. This ratio will be dependent on the current pool price as well as the position's selected range.
* Swap USDC -> WETH
* Add the exact amounts of the remaining USDC and the newly swapped WETH

Note that throughout the above process, swaps as well as liquidity additions are exposed to [slippage](slippage.md) risks(as well as [price impact](price-impact.md) for swaps). As such, the amount added is rarely ever exact which results in unpredictable amounts of tokens being left in your wallet. If this is a significant amount, not only will you be losing out on potential yield but you would have to repeat the above process again, incurring double the amount of gas fees.&#x20;

## Solution: One Click Zap

To improve the liquidity provider user experience, zaps enable LPs to conveniently achieve all the above in a single click. In other words, zaps allow users to add/remove liquidity to AMM pools with just a single token by signing a single transaction.

Following on the example above, there are 2 directions for zaps:

* **Zap In** (add liquidity): If you are providing 1,000USDC to the USDC-WETH pool, zapping in allows you to send 1,000USDC to the contract and receive the position NFT in return. A portion of the 1,000USDC will be converted to WETH and added to the pool depending on the pool price relative to your selected position range. The exact proportion can be derived from your position NFT.
* **Zap Out** (remove liquidity): When removing liquidity, you can also choose to zap out and receive one of the pool's tokens. In this case, your position NFT value (i.e. total value of USDC & WETH) will be converted to USDC and returned to your wallet.

In both the above cases, LPs are less likely to face any slippage risks as the whole process is completed within a single transaction. Consequently, there is also no longer a need to conduct additional transactions which incur both more gas fees and manual management.

{% hint style="success" %}
**Maximizing Returns With Elastic Zap**

KyberSwap has iterated upon the zap concept, enabling LPs to zap into Elastic pools! Please refer to [Elastic Zap](../../../liquidity-solutions/kyberswap-elastic/concepts/elastic-zap.md) for more information on how this innovation could maximize your LP returns.
{% endhint %}
