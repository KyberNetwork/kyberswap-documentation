---
description: KyberSwap Aggregator EVM APIs
---

# EVM Swaps

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.3.yaml" %}

{% hint style="success" %}
#### Note on integrations: clientID

In order to continuously improve the KyberSwap Aggregator, our APIs implement a client identifier field that enables us to understand how the APIs are being utilized. As a developer integrating with our APIs, **please add your clientID (i.e. company name) to the `x-client-id` field in the API header** to enable us to serve you better.

For integrators who have previously specified your clientID under the `clientData`/`source` fields in the query params, we highly encourage using the `x-client-id` in the headers instead. As KyberSwap continues to optimize our Aggregator API,  support for reading clientID from the query params will be deprecated.

#### Example

* \[V2]`GET/POST` Header
  * x-client-id="yourCompanyNameHere"
{% endhint %}

## EVM swap APIs

If you're just getting started with the KyberSwap Aggregator, you can refer to our [Execute A Swap With The Aggregator API](../developer-guides/execute-a-swap-with-the-aggregator-api.md) dev guide for information and code samples on how to query and execute swaps at the best rates. Note that there is also a [KyberSwap Widget](../../kyberswap-widget/) option for integrators who require a simple minimal-code implementation. For existing integrators, please refer to [Upgrading From APIv1 To APIv2](../developer-guides/upgrading-from-apiv1-to-apiv2.md) for further details on the motivation behind the upgrade as well as the relevant changes to swap flow and parameters.&#x20;

To support more performant queries, KyberSwap highly encourages all integrators to implement the latest API `[V2]` version. While both versions of the API remains backwards compatible, only the `[V2]` APIs will continue to receive updates and hence developers are highly encouraged to implement the latest `[V2]` APIs to avoid any disruptions as the `[V1]` API will eventually be deprecated.

{% hint style="info" %}
#### ZkSync Era support

For integrators looking to build on top of the KyberSwap Aggregator on ZkSync Era (ChainID: 324), please note that only the `[V2]` API is supported.
{% endhint %}

### API \[V2]: Latest

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.3.yaml" path="/{chain}/api/v1/routes" method="get" %}
[KyberSwapAggregator_EVMAPIs_v2.3.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.3.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.3.yaml" path="/{chain}/api/v1/route/build" method="post" %}
[KyberSwapAggregator_EVMAPIs_v2.3.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.3.yaml)
{% endswagger %}

### API \[V1]: Sunset period

{% swagger src="../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.3.yaml" path="/{chain}/route/encode" method="get" %}
[KyberSwapAggregator_EVMAPIs_v2.3.yaml](../../../.gitbook/assets/KyberSwapAggregator_EVMAPIs_v2.3.yaml)
{% endswagger %}
