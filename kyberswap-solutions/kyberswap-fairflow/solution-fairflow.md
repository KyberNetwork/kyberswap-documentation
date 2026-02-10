# Solution (FairFlow)

### Return Opportunity Value Loss From Arbitrage To LPs

Instead of allowing arbitrage profits to be fully captured by external arbitrageurs, FF redirects these profits back to LPs - known as Equilibrium Gain (EG) - through EG Sharing Program.

This is made possible because the KyberSwap Aggregator is the only taker for FF pools, blocking external arbitrageurs from fully extracting value. As a result, the majority of arbitrage profits generated within FF pools are captured by the FF hook and then redistributed to LPs.

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Here’s a simple explanation and example to help you understand how FF works:

* A user wants to trade 10,000 USDC for ETH via KyberSwap Aggregator.
* Behind the scenes, the KyberSwap Aggregator checks prices across various pools and FF pools to determine that the fair market output should be 3.88 ETH.
* If the FF pools offer better output compared to the fair market output, KyberSwap Aggregator will ask FF pools signer for a signature of the fair market price. Then KyberSwap Aggregator will return to the taker the signature and a trading route that partially goes through the FF pools.
*   If part of the trade is routed through the FF pools - say 1,000 USDC - and that portion returns more than expected based on the signed reference (e.g. 0.40 ETH instead of 0.388 ETH), the difference (0.012 ETH) is recognized as Equilibrium Gain (EG).

    _Note: From the beginning, the taker received a quote that includes the fair market output so 0.388 is what they expected_
* In this case, KyberSwap Aggregator is the only taker for FF pool so this Equilibrium Gain (EG) is absorbed by FF hook, rather than going to external arbitragers, and later redistributed to LPs via EG Sharing Program.

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

**How is Equilibrium Gain (EG) actually distributed back to LPs?**

The total EG is split into two parts:

* EG Sharing Program (70%): Distributed to each position proportionally to its EG contribution.
* Platform (30%): Allocated to the platform, which may distribute it to Partners (Token teams & Platforms), KyberSwap, KyberDAO or reserve it for LM program and other future rewards.

Positions earn an **EG Sharing** based on their contributed EG. EG Sharing Program directly distributes rewards in the two tokens of the token pair, and the cycle for EG distribution is on a weekly basis.

_Note: The EG Sharing Program structure may be revised in the future._



### Earn EG Rewards Without Sacrificing Other Utilities

Since EG Sharing Program (also LM Program) doesn’t require LPs to stake their LP tokens in a farming contract to receive EG Sharing (and also LM reward), they can freely use those LP tokens in other DeFi protocols to earn additional yield.

For example:

* An LP holds a USDC/ETH LP token: 0x2AC03BF434db503f6f5F85C3954773731Fc3F056.
* They can claim their EG Sharing on KyberSwap in both tokens of the pair, without needing to stake the LP token.
* At the same time, the LP token can be used elsewhere - such as lending or staking platforms - for further yield opportunities and utility.

This flexibility is made possible by FFs off-chain reward mechanism. Unlike traditional AMMs where rewards are calculated via on-chain farming contracts, FF tracks LP participation off-chain and distributes EG Sharing to LP token holders. This design also helps reduce staking-related risks for LPs, as no staking is needed.
