---
description: DeFi's Open and Permissionless Liquidity Backbone
cover: .gitbook/assets/KyberSwap_Banner.png
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Introduction to KyberSwap

**KyberSwap** is a multi-chain decentralized solution developed within Kyber Network Ecosystem, offering advanced trading tools and a comprehensive suite of earning opportunities across EVM blockchain networks. Built on [decentralized finance](https://docs.kyberswap.com/getting-started/foundational-topics/decentralized-finance) (DeFi) principles of open access, KyberSwap serves human users through the interface, builders and developers through open APIs, and AI agents through pre-built skills and an MCP server.

Through KyberSwap Interface (”Services”), users can access a full suite of on-chain trading tools - swap, limit order, cross-chain swap - alongside Kyber Earn, a hub to explore and manage earning opportunities. For developers and builders, KyberSwap offers a set of open, permissionless integration services to build decentralized trading and liquidity tools into their own dApps. KyberSwap also provides pre-built skills and an MCP server for developers and AI agents to interact with KyberSwap's on-chain infrastructure for data queries, automated trading, and liquidity provision tools.

KyberSwap connects to over [420+ liquidity sources across 17 chains](https://docs.kyberswap.com/getting-started/supported-exchanges-and-networks), serving as DeFi's open and permissionless liquidity backbone. With hundreds of projects building on top of KyberSwap, our solutions have facilitated over US$150B in transactions for more than 4.6M users, consistently ranking #1 on EVM by trading volume.

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3>👤 User Guide</h3></td><td>Learn how to use KyberSwap products and features step by step</td><td><a href=".gitbook/assets/user-guide.png">user-guide.png</a></td><td><a href="https://app.gitbook.com/s/w1XgQJc40kVeGUIxgI7c/user-guide">User Guide</a></td></tr><tr><td><h3>🛠 Developer Guide</h3></td><td>Learn how to integrate with KyberSwap API</td><td><a href=".gitbook/assets/developer.png">developer.png</a></td><td><a href="https://app.gitbook.com/s/w1XgQJc40kVeGUIxgI7c/developer-guide">Developer Guide</a></td></tr><tr><td><h3>🤖 AI Agent Hub</h3></td><td>Resources and tools that enable AI agents to interact with KyberSwap</td><td><a href=".gitbook/assets/ai-agent.png">ai-agent.png</a></td><td><a href="https://app.gitbook.com/s/w1XgQJc40kVeGUIxgI7c/ai-agent-hub">AI Agent Hub</a></td></tr></tbody></table>

## KyberSwap Solutions

### KyberSwap Interface (”Services”)

[**KyberSwap Interface**](https://kyberswap.com/): A one-stop [interface](https://kyberswap.com/) that provides convenient and open access to KyberSwap's trading tools and earning opportunities within the DeFi ecosystem. Through the interface, users can access core functionalities, including [Swap](https://docs.kyberswap.com/user-guide/swap) (powered by KyberSwap Aggregator), [Limit Order](user-guide/limit-order/), [Cross-chain Swaps](https://docs.kyberswap.com/user-guide/cross-chain-swap), [Kyber Earn](user-guide/kyber-earn/) (powered by [ZaaS](https://docs.kyberswap.com/developer-guide/zap-as-a-service-zaas-api)), [Campaigns](https://kyberswap.com/campaigns), and other supported features.

* [**Swap**](https://docs.kyberswap.com/user-guide/swap): Instantly swap tokens at superior rates, powered by the KyberSwap Aggregator. Connected to over 420+ liquidity sources across 17 chains, the Aggregator [splits and reroutes trades](developer-guide/start-here/foundational-solutions/dynamic-trade-routing.md) through capital-efficient sources, ensuring the best swap rates while encouraging greater market stability. Swaps are further enhanced by [Smart Settlement](developer-guide/start-here/foundational-solutions/smart-settlement-better-swap-output-with-lower-slippage.md), which compares candidate pools on-chain at execution time to maximize token output, minimize slippage, and protect against PropAMM spoofing — with no extra steps or fees.
* [**Limit Order**](https://docs.kyberswap.com/user-guide/limit-order): Allows users to set preferred swap rates and execute gasless, slippage-free, and zero-fee trades powered by our wide network of takers. Orders are [automatically settled on-chain](developer-guide/start-here/foundational-solutions/off-chain-relay.md) only when predefined conditions are met. Users retain full ownership of their assets until a matching trade is found.
* [**Cross-chain Swap**](https://docs.kyberswap.com/user-guide/cross-chain-swap): Enables users to transfer and exchange assets across [23 supported blockchain networks](getting-started/supported-exchanges-and-networks.md), including non-EVM and EVM chains. KyberSwap aggregates quotes from multiple third-party cross-chain providers, automatically selecting the best rate while giving users full transparency to compare routes, fees, and estimated arrival times.
* [**Kyber Earn**](user-guide/kyber-earn/): A streamlined, all-in-one platform designed to help users easily access and manage yield-generating opportunities across multiple liquidity protocols. By aggregating top-tier protocols, Kyber Earn provides a single interface where users can explore, compare, enter positions with ease via [Zap](developer-guide/zap-as-a-service-zaas-api/) technology, and track and manage their positions.
  * [**KyberSwap FairFlow**](user-guide/kyberswap-fairflow/): A swap hook built on Uniswap V4, PancakeSwap Infinity, and similar protocols that enhances liquidity pools, designed to help LPs earn additional yields from arbitrage value captured by external MEV bots. The captured value is redistributed back to LPs through the Equilibrium Gain (EG) Sharing Program, with no LP token staking required.
  * [**Smart Exit**](user-guide/smart-exit/): The industry's first intent-based execution model for liquidity management, enabling LPs to set conditional withdrawal rules on Kyber Earn - target pool price, fee threshold, or specific time - and have their positions exited automatically when conditions are met. Gasless and trustless, with smart contracts audited by Hexens.
* [**Campaigns**](https://kyberswap.com/campaigns): Trading campaigns and contests hosted directly on the KyberSwap Interface, giving users a chance to earn various rewards for participation.
* [**Market**](https://kyberswap.com/market-overview): Displays token buy and sell prices directly on the KyberSwap Interface, powered by [KyberSwap On-chain Price Service](developer-guide/start-here/foundational-solutions/kyberswap-onchain-price-service.md). Prices are based on real on-chain liquidity and refreshed every 10 seconds, providing network-specific pricing that reflects actual market conditions on each supported chain.

### KyberSwap Integrations

KyberSwap provides multiple core services for on-chain integration for building on-chain trading and liquidity features, plus supporting services. All KyberSwap APIs are public and do not require authentication. Refer to [Start Here](developer-guide/start-here/) for prerequisites, rate limits, and supported chains.

* [**KyberSwap Aggregator**](https://docs.kyberswap.com/developer-guide/aggregator-api): The engine behind KyberSwap's swap functionality. Connected to over 420+ liquidity sources across 17 chains, the Aggregator [splits and reroutes trades](https://docs.kyberswap.com/developer-guide/start-here/foundational-solutions/dynamic-trade-routing) through capital-efficient sources, ensuring optimal swap rates while encouraging greater market stability. Swaps are further enhanced by [Smart Settlement](developer-guide/start-here/foundational-solutions/smart-settlement-better-swap-output-with-lower-slippage.md), which compares candidate pools on-chain at execution time to maximize token output, minimize slippage, and protect against manipulation.
  * Aggregator API: Provides developers and builders with fine-tuned control when integrating swap functionality within their dApps. Guidelines and code samples are provided on how to [query and execute swaps](developer-guide/aggregator-api/how-to-guides/execute-a-swap-with-the-aggregator-api/).
  * [**KyberSwap Widget**](developer-guide/aggregator-api/how-to-guides/kyberswap-widget/): A plug-and-play, customizable swap interface that integrators can embed into their dApps with just a few lines of code — with configurable trade routes, fees, and themes.
* [**KyberSwap Limit Order**](https://docs.kyberswap.com/developer-guide/limit-order-api): The engine behind KyberSwap's limit order functionality, secured by [off-chain relay, on-chain settlement](developer-guide/start-here/foundational-solutions/off-chain-relay.md). Makers create and cancel orders gaslessly via EIP-712 signed messages; Takers query the order book and settle orders on-chain when predefined price conditions are met.
  * [**Limit Order API**](developer-guide/limit-order-api/): A set of [General](developer-guide/limit-order-api/api-reference/general-api.md), [Maker](developer-guide/limit-order-api/api-reference/maker-api.md), and [Taker](developer-guide/limit-order-api/api-reference/taker-api.md) APIs for developers and builders to integrate gasless limit order functionality into their dApps. KyberSwap provides the relevant APIs to encode the call data to be sent to the Limit Order smart contracts.
* [**Zap as a Service (ZaaS) API**](developer-guide/zap-as-a-service-zaas-api/): The engine behind KyberSwap's liquidity provision, powering Kyber Earn. ZaaS streamlines adding and removing liquidity by allowing users to enter or exit any concentrated liquidity position using any single token - without manually calculating token ratios. Powered by KyberSwap Aggregator, Zap minimizes price impact and employs fallback logic to execute additional swaps when necessary, maximizing capital efficiency even during volatile market conditions.
  * [**ZaaS API**](developer-guide/zap-as-a-service-zaas-api/): Provides developers and builders with programmatic access to Zap functionality for their dApps. Available via both [HTTP REST](developer-guide/zap-as-a-service-zaas-api/api-reference/zaas-http-api.md) and [gRPC](developer-guide/zap-as-a-service-zaas-api/api-reference/zaas-grpc-api.md).
  * [**Liquidity Widget**](developer-guide/zap-as-a-service-zaas-api/how-to-guides/kyberswap-liquidity-widget/): A plug-and-play widget that integrators can embed to let users provide liquidity efficiently within their dApps - powered by ZaaS.
* [**KyberSwap On-chain Price Service**](developer-guide/start-here/foundational-solutions/kyberswap-onchain-price-service.md): The foundational solution behind all KyberSwap services. Provides accurate, reliable, and tradable price information for a wide range of tokens. Unlike services that aggregate prices into a single average, KyberSwap delivers network-specific prices based on real on-chain liquidity, ensuring prices are reflective of actual market conditions on each supported chain.
* [**AI Agent Hub**](ai-agent-hub/overview.md): Resources and tools that enable AI agents to interact with KyberSwap APIs for trading, managing liquidity, and querying DeFi data across 18 EVM chains. Includes [Skills](ai-agent-hub/skills-for-local-agents.md) (pre-built markdown instructions for local AI coding agents using `curl` and `cast`) and an [MCP Server](ai-agent-hub/mcp-server-for-hosted-agents.md) for hosted agents. No API keys required.

### Liquidity Solutions <mark style="color:orange;">**(deprecated)**</mark>

{% hint style="warning" %}
**KyberSwap Elastic Security Incident**

On 22 Nov 2023, the Elastic protocol experienced a security incident. More details can be found via our [official channels](https://x.com/KyberNetwork?s=20).
{% endhint %}

* KyberSwap Classic
* KyberSwap Elastic

