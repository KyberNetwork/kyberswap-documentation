---
description: KyberSwap Aggregator EVM APIs
---

# EVM Swaps

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.5.0.yaml" %}

{% hint style="success" %}
#### Note on integrations: clientID

In order to continuously improve the KyberSwap Aggregator, our APIs implement a client identifier field that enables us to understand how the APIs are being utilized. As a developer integrating with our APIs, **please add your clientID (i.e. company name) to the `x-client-id` field in the API header** to enable us to serve you better.

For integrators who have previously specified your clientID under the `clientData`/`source` fields in the query params, we highly encourage using the `x-client-id` in the headers instead. As KyberSwap continues to optimize our Aggregator API,  support for reading clientID from the query params will be deprecated.

#### Example

* \[V1]`GET/POST` Header
  * x-client-id="yourCompanyNameHere"
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

### `Latest`

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.5.0.yaml" path="/{chain}/api/v1/routes" method="get" %}
[KyberSwapAggregator_EVMAPIs_v2.5.0.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.5.0.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.5.0.yaml" path="/{chain}/api/v1/route/build" method="post" %}
[KyberSwapAggregator_EVMAPIs_v2.5.0.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.5.0.yaml)
{% endswagger %}

### `Legacy`

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.5.0.yaml" path="/{chain}/route/encode" method="get" %}
[KyberSwapAggregator_EVMAPIs_v2.5.0.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.5.0.yaml)
{% endswagger %}
