---
description: Everything you need before your first API call
---

# Start Here

KyberSwap provides three APIs for building on-chain trading and liquidity features - the [Aggregator API](../aggregator-api/) for instant token swaps, the [Zap as a Service (ZaaS) API](../zap-as-a-service-zaas-api/) for streamlined liquidity provision, and the [Limit Order API](../limit-order-api/) for gasless and price-conditional trades. This section covers everything that applies across all three: how to choose the right API, usage limits, supported chains, and the core solutions behind how they work.

## Which API Should I Use?

KyberSwap offers 3 APIs. Find your use case in the table below.

<table><thead><tr><th width="492.3203125">I want to...</th><th>Use this</th></tr></thead><tbody><tr><td>Swap token A → token B at the best available rate</td><td><a href="../aggregator-api/">Aggregator API</a></td></tr><tr><td>Swap token A → token B at a price I set</td><td><a href="../limit-order-api/">Limit Order API</a></td></tr><tr><td>Add liquidity to a supported pool using any token</td><td><a href="../zap-as-a-service-zaas-api/">Zap as a Service API</a></td></tr><tr><td>Remove liquidity and receive a single token</td><td><a href="../zap-as-a-service-zaas-api/">Zap as a Service API</a></td></tr><tr><td>Migrate from a position to a new position</td><td><a href="../zap-as-a-service-zaas-api/">Zap as a Service API</a></td></tr><tr><td>Fill open limit orders as a taker or arbitrage bot</td><td><a href="../limit-order-api/">Limit Order API</a></td></tr></tbody></table>

* [**KyberSwap Aggregator** **API**:](../aggregator-api/) Provides developers with more fine-tuned control when integrating swap functionality within their app. We provide guidelines and code samples on how to query and execute swaps at the favourable rates.
  * [**KyberSwap Widget**](../aggregator-api/how-to-guides/kyberswap-widget/): Plug and play superior rates directly from your app with just a few lines of code. Our [endlessly customizable widget](https://app.gitbook.com/o/2RCW3YGZHRsvcw6VtGeF/s/w1XgQJc40kVeGUIxgI7c/kyberswap-solutions/kyberswap-widget/developer-guides/customizing-the-kyberswap-widget) enables integrators to seamlessly blend superior rates into their dApps with easily configurable trade routes, fees, and themes.
* [**Limit Order API:**](https://docs.kyberswap.com/kyberswap-solutions/limit-order/developer-guides) A set of [Maker](../limit-order-api/#maker) and [Taker](../limit-order-api/#taker) APIs enables gasless management of limit orders secured by the option to settle on-chain. When settling orders on-chain, KyberSwap Limit Order provides the relevant APIs required to encode the call data to be sent to the Limit Order smart contracts.
* [**KyberSwap Zap as a Service (ZaaS)**](../zap-as-a-service-zaas-api/): An API that streamlines decentralized liquidity provision. Powered by [KyberSwap Aggregator](../aggregator-api/), Zap minimizes price impact and employs fallback logic to execute additional swaps when necessary - maximizing capital efficiency and reducing failure rates, even during volatile market conditions.

## Rate Limits & Client ID

KyberSwap APIs do not require authentication. Include `x-client-id` header in every request, using your app or company name as the value. Refer to [Rate Limits & Client ID](rate-limits-and-client-id.md) for further details.



## Supported Chains & Networks

All KyberSwap APIs are EVM-only. Each API is available on a different subset of chains. See [Supported Chains & Networks](../../getting-started/supported-exchanges-and-networks.md) for the full list, including the chain identifier strings required in API paths.



## Foundational Solutions

A short set of solutions that explain why the APIs are designed the way they are - covering trade routing, off-chain relay, and gasless approvals. If you're new to KyberSwap's architecture, read these before integrating. See [Foundational Solutions](foundational-solutions/).
