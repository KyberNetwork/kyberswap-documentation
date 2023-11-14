---
description: KyberSwap Aggregator EVM APIs
---

# EVM Swaps

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.8.1.yaml" %}

{% hint style="success" %}
#### Note on integrations: clientID

In order to continuously improve the KyberSwap Aggregator, our APIs implement a client identifier field that enables us to understand how the APIs are being utilized. As a developer integrating with our APIs, **please use the same clientID (i.e. company name)** for:

* **\[V1] Get Swap Route**
  * **Header:** `x-client-id`
  * **Parameters:** `source`
* **\[V1] Post Swap Route For Encoded Data**
  * **Header:** `x-client-id`
  * **Body:** `source`

This will enable us to serve you better as we continuously strive to improve our Aggregator API. For integrators who have previously integrated with our `Legacy` API, we highly encourage migrating to the `Latest` APIs to ensure access to the latest features as well as improved service quality and efficiency.

#### Example

* \[V1]`GET`
  * Header
    * x-client-id="yourCompanyNameHere"
  * Parameter
    * source="yourCompanyNameHere"
* \[V1] POST
  * Header
    * x-client-id="yourCompanyNameHere"
  * Body
    * source="yourCompanyNameHere"
{% endhint %}

## EVM swap APIs

If you're just getting started with the KyberSwap Aggregator, you can refer to our [Execute A Swap With The Aggregator API](../developer-guides/execute-a-swap-with-the-aggregator-api.md) dev guide for information and code samples on how to query and execute swaps at superior rates. Note that there is also a [KyberSwap Widget](../../kyberswap-widget/) option for integrators who require a simple minimal-code implementation. For existing integrators, please refer to [Upgrading To APIv1](../developer-guides/upgrading-to-apiv1.md) for further details on the motivation behind the upgrade as well as the relevant changes to swap flow and parameters.&#x20;

To support more performant queries, KyberSwap highly encourages all integrators to implement the latest API `[V1]` version. While both versions of the API remains backwards compatible, only the `[V1]` APIs will continue to receive updates and hence developers are highly encouraged to implement the latest `[V1]` APIs to avoid any disruptions as the non-versioned API will eventually be deprecated.

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

The Aggregator APIs require a chain name to be included in the path when calling the APIs:&#x20;

* Ethereum (ChainID: 1) -> `ethereum`
* BSC (ChainID: 56) -> `bsc`
* Arbitrum (ChainID: 42161) -> `arbitrum`
* Polygon PoS (ChainID: 137) -> `polygon`
* Optimism (ChainID: 10) -> `optimism`
* Avalanche (ChainID: 43114) -> `avalanche`
* Base (ChainID: 8453) -> `base`
* Cronos (ChainID: 25) -> `cronos`
* zkSync Era (ChainID: 324) -> `zksync`
* Fantom (ChainID: 250) -> `fantom`
* Linea (ChainID: 59144) -> `linea`
* Polygon zkEVM (ChainID: 1101) -> `polygon-zkevm`
* Aurora (ChainID: 1313161554) -> `aurora`
* BitTorrent Chain (ChainID: 199) -> `bittorrent`
* Scroll (ChainID: 534352) -> `scroll`
{% endhint %}

### `Latest`

<figure><img src="../../../.gitbook/assets/Aggregator APIv1.jpg" alt=""><figcaption></figcaption></figure>

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.8.1.yaml" path="/{chain}/api/v1/routes" method="get" %}
[KyberSwapAggregator_EVMAPIs_v2.8.1.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.8.1.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.8.1.yaml" path="/{chain}/api/v1/route/build" method="post" %}
[KyberSwapAggregator_EVMAPIs_v2.8.1.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.8.1.yaml)
{% endswagger %}

### `Legacy`

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.8.1.yaml" path="/{chain}/route/encode" method="get" %}
[KyberSwapAggregator_EVMAPIs_v2.8.1.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.8.1.yaml)
{% endswagger %}
