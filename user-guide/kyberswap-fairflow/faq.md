---
description: Frequently Asked Questions about KyberSwap FairFlow
---

# FAQ

**Is FairFlow safe? Who holds the funds?**

Funds are held directly in Uniswap V4's and similar protocols' pools, not by KyberSwap, FairFlow only adds a swap hook layer to control taker access and absorb EG, which does not add any security issues to LPs. You can refer to this document for reference: [https://docs.uniswap.org/contracts/v4/quickstart/hooks/swap](https://docs.uniswap.org/contracts/v4/quickstart/hooks/swap)

FairFlow hook smart contract is audited by [Omniscia](https://x.com/Omniscia_sec).



**How can I claim my EG Sharing?**

To claim EG Sharing, your wallet must hold the LP token at the time of claiming. If staked elsewhere, please unstake it first.



**Is FairFlow only applicable on Uniswap v4 and Pancakeswap v4?**

No. FairFlow initially launched on Uniswap V4 and Pancakeswap V4 pools, but we plan to expand support to other similar protocols in the future.



**Can the EG Sharing Program change over time?**

Yes. The EG Sharing Program, funded by the FairFlow hook, is subjected to constant evaluation and re-adjustment.



**How is the EG Sharing Program different from a Liquidity Mining Program?**&#x20;

Yes, they are different. The EG Sharing Program is funded by actual arbitrage opportunity (real cash flow), while traditional Liquidity Mining programs mainly rely on short-term token incentives provided by the project.



**Can FairFlow run a Liquidity Mining Program alongside the EG Sharing Program?**

Yes, FairFlow can run a Liquidity Mining Program alongside the EG Sharing Program. Our objective is to maximize value for Liquidity Providers (LPs). KyberSwap will continuously evaluate high-potential pools and, when feasible, launch supplementary Liquidity Mining campaigns. We may also engage with strategic partners to co-fund these initiatives and further enhance LP yields.



**How does the KyberSwap Aggregator ensure the best rate for takers while Equilibrium Gain (EG) is absorbed?**

A FairFlow pool is included in the routing only when it offers a better rate than existing liquidity sources and adds value to the quoted rate. The FairFlow hook captures only a portion of this added value as Equilibrium Gain (EG), ensuring that takers still receive a superior output compared to routes that don’t include FairFlow.



**Does limiting FairFlow access to the KyberSwap Aggregator restrict takers from interacting with it?**

No, it does not. Even though only KyberSwap Aggregator is allowed to swap with FairFlow, the KyberSwap Aggregator is available for all takers and currently one of the top aggregators with good market share, and have been integrated into major platforms/wallets/solvers/fillers, etc.



**Will FairFlow hook be available for pools not created by Kyber?**&#x20;

Not at this time, but it is part of our development roadmap. We plan to release further details and timelines once the implementation plans are finalized.
