---
description: KyberSwap Aggregator EVM APIs
---

# EVM Swaps

{% hint style="info" %}
_Disclaimer: Data provided as-is. Please see the relevant_ [_Developer Guide_](../developer-guides/execute-a-swap-with-the-aggregator-api.md#overview) _for more details_
{% endhint %}

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.12.0.yaml" %}

{% hint style="success" %}
**Note on integration: clientID**

In order to continuously improve the KyberSwap Aggregator, our APIs implement a client identifier field that enables us to understand how the APIs are being utilized. A stricter rate limit will be applied if a clientId is not provided. As a developer integrating with our APIs, **please preferably use the same clientID (i.e. company name or your app name)** for:

* **\[V1] Get Swap Route**
  * **Header:** `x-client-id`
* **\[V1] Post Swap Route For Encoded Data**
  * **Header:** `x-client-id`

This will enable us to serve you better as we continuously strive to improve our Aggregator API. For integrators who have previously integrated with our `Legacy` API, we highly encourage migrating to the `Latest` APIs to ensure access to the latest features as well as improved service quality and efficiency.

**Example**

* \[V1] `GET` /routes
  * Header
    * `x-client-id: MyAwesomeApp`
* \[V1] `POST` /route/build
  * Header
    * `x-client-id: MyAwesomeApp`
{% endhint %}

## EVM swap APIs

If you're just getting started with the KyberSwap Aggregator, you can refer to our [Execute A Swap With The Aggregator API](../developer-guides/execute-a-swap-with-the-aggregator-api.md) dev guide for information and code samples on how to query and execute swaps at superior rates. Note that there is also a [KyberSwap Widget](../../kyberswap-widget/) option for integrators who require a simple minimal-code implementation. For existing integrators, please refer to [Upgrading To APIv1](../developer-guides/upgrading-to-apiv1.md) for further details on the motivation behind the upgrade as well as the relevant changes to swap flow and parameters.

To support more performant queries and the use of RFQ liquidity sources, KyberSwap highly encourages all integrators to implement the latest API `[V1]` version. While both versions of the API remains backwards compatible, only the `[V1]` APIs will continue to receive updates and can make use of RFQ liquidity sources, and hence developers are highly encouraged to implement the latest `[V1]` APIs to avoid any disruptions as the non-versioned API will eventually be deprecated.

{% hint style="info" %}
\[V1] `GET` `/routes` API is designed to be performant and real-time, the market moves constantly so it is recommended to not cache routes from client side for more than 5-10 seconds and to refetch a new route before swapping if the current swap is too long ago to avoid potential slippage.
{% endhint %}

<details>

<summary>API statuses and support</summary>

KyberSwap APIs uses the following statuses to minimize version miscommunications and ensure an uninterrupted service for the end user:

* `Latest`: API is functional and supported. This is the recommended version for all integrators (new and existing).
* `Legacy`: API remains functional with support for bugs only. No new feature updates.
* `Deprecated`: API is no longer functional and is not supported.

For all developers, it is highly recommended that you refer to the API with the `Latest` tag to ensure access to the latest features as well as improved service quality and efficiency. APIs which are planned to be sunset will be tagged `Legacy` during the transition period and thereafter moved to `Deprecated`.

The KyberSwap Docs will continue to maintain information regarding `Legacy` and `Deprecated` APIs.

</details>

{% hint style="info" %}
**Chain identifiers**

The Aggregator APIs require a chain **name** to be included in the path when calling the APIs:

* Ethereum (ChainID: 1) -> `ethereum`
* BSC (ChainID: 56) -> `bsc`
* Arbitrum (ChainID: 42161) -> `arbitrum`
* Polygon PoS (ChainID: 137) -> `polygon`
* Optimism (ChainID: 10) -> `optimism`
* Avalanche (ChainID: 43114) -> `avalanche`
* Base (ChainID: 8453) -> `base`
* Linea (ChainID: 59144) -> `linea`
* Mantle (ChainID: 5000) -> `mantle`
* Sonic (ChainID: 146) -> `sonic`
* Berachain (ChainID: 80094) -> `berachain`
* Ronin (ChainID: 2020) -> `ronin`
* Unichain (ChainID: 130) -> `unichain`
* HyperEVM (ChainID: 999) -> `hyperevm`
{% endhint %}

### &#x20;Latest

<figure><img src="../../../.gitbook/assets/Aggregator APIv1.jpg" alt=""><figcaption></figcaption></figure>

{% openapi-operation spec="aggregator-api" path="/{chain}/api/v1/routes" method="get" %}
[OpenAPI aggregator-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/7021a94270560f8aab4e6c37f0a65892f33d03e1a42e077686016fa7ab9fafc4.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250922%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250922T085931Z&X-Amz-Expires=172800&X-Amz-Signature=bf35872bfbb29ef2b86e39e4935cdf4486d7a8beaa327f807b4608e0cf54685d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="aggregator-api" path="/{chain}/api/v1/route/build" method="post" %}
[OpenAPI aggregator-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/7021a94270560f8aab4e6c37f0a65892f33d03e1a42e077686016fa7ab9fafc4.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250922%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250922T085931Z&X-Amz-Expires=172800&X-Amz-Signature=bf35872bfbb29ef2b86e39e4935cdf4486d7a8beaa327f807b4608e0cf54685d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### Legacy

{% openapi-operation spec="aggregator-api" path="/{chain}/route/encode" method="get" %}
[OpenAPI aggregator-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/7021a94270560f8aab4e6c37f0a65892f33d03e1a42e077686016fa7ab9fafc4.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250922%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250922T085931Z&X-Amz-Expires=172800&X-Amz-Signature=bf35872bfbb29ef2b86e39e4935cdf4486d7a8beaa327f807b4608e0cf54685d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% hint style="info" %}
**KyberSwap positive slippage surplus collection**

For every swap executed by the KyberSwap Aggregator, users will be able to see an estimated output amount based on the current price as well as a minimum received that takes into account the [max slippage setting](../../kyberswap-interface/user-guides/instantly-swap-at-superior-rates.md#customizing-trade-parameters). KyberSwap Aggregator will always strive to execute swaps at the estimated output amount and revert the transaction if the minimum received amount is not achieved.

In the event that the market moves in favor of the trade which results in a surplus of tokens above the estimated output amount (i.e positive slippage), this surplus will initially accrue to KyberSwap. Surplus sharing programs will be explored as the KyberSwap ecosystem grows to be more self-sufficient. **Critically, traders will always get the estimated output amount as long as the swap is executed at or above the current rate**.

Note that this surplus is different from fees as it only applies in cases where the executed swap rate is better than the estimated rate at point of transaction confirmation. Please refer to [slippage](../../../getting-started/foundational-topics/decentralized-finance/slippage.md) for more information.
{% endhint %}
