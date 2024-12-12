---
description: >-
  Introducing Zap as a Service API (ZaaS) and Liquidity Widget, streamlining
  decentralized liquidity provision. Effortlessly add liquidity with a single
  token for enhanced DeFi engagement.
---

# KyberSwap Zap as a Service

The objective of the Zap as a Service API (ZaaS) / Zap Liquidity Widget is to enable users to effortlessly add liquidity into any concentrated liquidity protocol using any tokens, while also minimizing price impact through integration with the KyberSwap aggregator.

Currently, participating in concentrated liquidity protocols such as Uniswap v3 entails a cumbersome process of manually calculating specific token ratios based on position ranges, followed by separate transactions for swapping and depositing into the pool. We aim to streamline this process, making it as simple as a token swap.

The target audience for the ZaaS API / Liquidity Widget includes portfolio management apps, wallets, and other liquidity protocol dapps seeking to integrate this API into their UI.

## Advantages

* **Streamlined Liquidity Provision:** Zap simplifies the process of adding liquidity into concentrated liquidity protocols, making participation as straightforward as a token swap, catering to users of all experience levels.
* **Minimized Price Impact:** By leveraging the KyberSwap aggregator swapping along with pool swapping and simulating different zapping routes, Zap reduces price impact during the liquidity provision, ensuring optimal price impact for user.
* **Capital Efficiency:** Zap employs fallback logic to execute additional swaps if necessary, ensuring maximal usage of capital during liquidity provision even during volatile market.
* **Integration Flexibility:** The ZaaS API aims to offer seamless integration into various dexes, enhancing user experience and competitiveness.

## Use cases

Zap currently supports the following liquidity actions:

1. Add Liquidity to a Pool with a new position
2. Increase Liquidity into an existing Liquidity Position

## Future developements

1. Creating a new pool - pool not created yet for the specific token pair-fee tier configuration
2. Remove liquidity from the pool into a single token
