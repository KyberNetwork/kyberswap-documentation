---
description: DeFi's Open and Permissionless Liquidity Backbone
cover: .gitbook/assets/KyberSwap_Banner.png
coverY: 0
---

# Introduction to KyberSwap

Kyber Network is building a world where anyone can freely, reliably and effortlessly trade their funds on their own terms. Founded on [decentralized finance](https://docs.kyberswap.com/getting-started/foundational-topics/decentralized-finance) (DeFi) principles of open access, KyberSwap is a multi-chain decentralized platform that offers advanced trading tools and a comprehensive suite of earning opportunities, enabling users to trade and earn without intermediaries through an open and permissionless experience.

With hundreds of projects building on top of KyberSwap, our solutions have facilitated over US$100B in transactions for more than 2.6M users (with totals continuing to increase). Serving as DeFi’s open and permissionless liquidity backbone, KyberSwap continues to expand its ecosystem and now connects to more than [420+ liquidity sources across 17 chains](https://docs.kyberswap.com/getting-started/supported-exchanges-and-networks).

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3>👤 User Guide</h3></td><td>Learn how to use KyberSwap products and features step by step</td><td><a href=".gitbook/assets/user-guide.png">user-guide.png</a></td><td><a href="/broken/pages/mxns8qL7odOMYPx9JS4K">Broken link</a></td></tr><tr><td><h3>🛠 Developer Guide</h3></td><td>Learn how to integrate with KyberSwap API</td><td><a href=".gitbook/assets/developer.png">developer.png</a></td><td><a href="/broken/pages/nCZc8jy0eOIOhoFPpzRy">Broken link</a></td></tr><tr><td><h3>🤖 AI Agent Hub</h3></td><td>Resources and tools that enable AI agents to interact with KyberSwap</td><td><a href=".gitbook/assets/ai-agent.png">ai-agent.png</a></td><td><a href="/broken/pages/HwWoi5ckULK1Pamf9iVM">Broken link</a></td></tr></tbody></table>

## KyberSwap Solutions

* [**KyberSwap Interface**](https://kyberswap.com/): A one-stop [web interface](https://kyberswap.com/) that provides convenient and open access to KyberSwap’s trading tools and earning opportunities within the DeFi ecosystem. Through the interface, users can access core functionalities, including [Swap](user-guide/swap/) (powered by KyberSwap Aggregator), [Limit Order](user-guide/limit-order/), [Cross-chain Swaps](user-guide/cross-chain-swap.md), Kyber Earn (powered by [ZaaS](developer-guide/zap-as-a-service-zaas-api/)), and other supported features.
* [**KyberSwap Aggregator**](developer-guide/aggregator-api/): Enables token swaps at the best rates with our intelligent trade route scanner. Connected to over 420+ liquidity sources across 17 chains, KyberSwap Aggregator [splits and reroutes trades](developer-guide/start-here/foundational-solutions/dynamic-trade-routing.md) through capital-efficient sources, thereby ensuring the best swap rates while encouraging greater market stability.
  * [**Aggregator API**](developer-guide/aggregator-api/): Provides developers with more fine-tuned control when integrating swap functionality within their app. We provide guidelines and code samples on how to query and execute swaps at the favourable rates.
  * [**KyberSwap Widget**](developer-guide/aggregator-api/how-to-guides/kyberswap-widget/): Plug and play superior rates directly from your app with just a few lines of code. Our [endlessly customizable widget](https://app.gitbook.com/o/2RCW3YGZHRsvcw6VtGeF/s/w1XgQJc40kVeGUIxgI7c/kyberswap-solutions/kyberswap-widget/developer-guides/customizing-the-kyberswap-widget) enables integrators to seamlessly blend superior rates into their dApps with easily configurable trade routes, fees, and themes.
* [**Limit Order**](user-guide/limit-order/): Allows users to set preferred swap rates and execute gasless, slippage-free, and zero-fee trades powered by our wide network of takers. Orders are [automatically settled on-chain](developer-guide/start-here/foundational-solutions/off-chain-relay.md) only when predefined conditions are met.
  * [**Limit Order API**](developer-guide/limit-order-api/)**:** A set of [Maker](developer-guide/limit-order-api/api-reference/maker-api.md) and [Taker](developer-guide/limit-order-api/api-reference/taker-api.md) APIs enables gasless management of limit orders secured by the option to settle on-chain. When settling orders on-chain, KyberSwap Limit Order provides the relevant APIs required to encode the call data to be sent to the Limit Order smart contracts.
* [**KyberSwap Cross-Chain Swaps**](user-guide/cross-chain-swap.md): Enables users to transfer and exchange assets across [23 supported blockchain networks](https://docs.kyberswap.com/getting-started/supported-exchanges-and-networks), including non-EVM and EVM chains. KyberSwap integrates with various third-party providers to suggest optimal rates and routes for cross-chain transactions.
* [**KyberSwap On-chain Price Service**](developer-guide/start-here/foundational-solutions/kyberswap-onchain-price-service.md): Provides accurate, reliable, and tradable price information for a wide range of tokens.
* [**KyberZap**](developer-guide/zap-as-a-service-zaas-api/): A technology that streamlines liquidity provision and withdrawal by enabling users to zap in with single or multiple tokens of their choice, zap out to any token, and migrate between positions.
  * [**KyberSwap Zap as a Service (ZaaS)**](https://app.gitbook.com/o/2RCW3YGZHRsvcw6VtGeF/s/w1XgQJc40kVeGUIxgI7c/kyberswap-solutions/kyberswap-zap-as-a-service): An API that streamlines decentralized liquidity provision. Powered by [KyberSwap Aggregator](developer-guide/aggregator-api/), Zap minimizes price impact and employs fallback logic to execute additional swaps when necessary - maximizing capital efficiency and reducing failure rates, even during volatile market conditions.
  * [**KyberSwap Liquidity Widget**](https://app.gitbook.com/o/2RCW3YGZHRsvcw6VtGeF/s/w1XgQJc40kVeGUIxgI7c/kyberswap-solutions/kyberswap-liquidity-widget): A plug-and-play widget that simplifies integration with KyberSwap ZaaS and enables users to provide liquidity more efficiently within integrated dApps.
* [**KyberSwap FairFlow**](https://docs.kyberswap.com/kyberswap-solutions/kyberswap-fairflow): A swap hook built on Uniswap V4, Pancakeswap Infinity, and similar protocols that enhances liquidity pools, designed to help LPs earn additional yields from arbitrage value captured by external MEV bots.

### Liquidity Solutions <mark style="color:orange;">**(deprecated)**</mark>

{% hint style="warning" %}
**KyberSwap Elastic Security Incident**

On 22 Nov 2023, the Elastic protocol experienced a security incident. More details can be found via our [official channels](https://x.com/KyberNetwork?s=20).

All other KyberSwap products ([Aggregator](kyberswap-solutions/kyberswap-aggregator/) & [Limit Order](kyberswap-solutions/limit-order/)) continue to be fully operational.
{% endhint %}

* <mark style="color:orange;">**KyberSwap Classic (deprecated)**</mark>: Amplify your returns through programmable pricing curves as well as dynamic auto-adjusting fees which responds to market conditions. Deposit your tokens into capitally efficient pools and let the protocol optimize trading spreads (i.e. fees) based on the market volatility. This service was <mark style="color:orange;">**discontinued on 26 March 2024.**</mark>
* <mark style="color:orange;">**KyberSwap Elastic (deprecated)**</mark>: Add liquidity into [customizable price ranges](reference/legacy/kyberswap-elastic/concepts/concentrated-liquidity.md) and [automatically compound your yields](reference/legacy/kyberswap-elastic/concepts/reinvestment-curve.md). Your concentrated liquidity positions are safeguarded against front-runners with our native [Anti-Sniping feature](reference/legacy/kyberswap-elastic/concepts/anti-sniping-mechanism.md). This service was <mark style="color:orange;">**discontinued on 23 November 2023.**</mark>

