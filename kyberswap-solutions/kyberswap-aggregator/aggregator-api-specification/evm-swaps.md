---
description: KyberSwap Aggregator EVM APIs
---

# EVM Swaps

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (3).yaml" %}

{% hint style="success" %}
#### Note on integrations: clientID

In order to continuously improve the KyberSwap Aggregator, our APIs implement a `clientData` or `source` field that enables us to understand how the APIs are being utilized. As a developer integrating with our APIs, **please add your clientID (i.e. company name) to the `clientData`/`source` fields** to enable us to serve you better.&#x20;

#### Example

* `[V1]GET`
  * clientData={"source":"yourCompanyNameHere"}
* `[V2]POST`
  * source="yourCompanyNameHere"
{% endhint %}

## EVM swap APIs

{% hint style="info" %}
#### More performant queries with \[V2] API and supporting future upgrades

Following feedback on the initial `[V1]` API, KyberSwap has implemented a more performant `[V2]` API which improves the response time for getting a route via offloading encoding requirements to the post method.

**Please refer to** [**Upgrading From APIv1 To APIv2**](../developer-guides/upgrading-from-apiv1-to-apiv2.md) **for further details on the motivation behind the upgrade as well as the relevant changes to swap flow and parameters.**

Please use the `[V2]GET` API for more efficient route queries. The returned route can then be reused in the `[V2]POST` body to get the encoded swap data. You can refer to [Execute A Swap With The Aggregator API](../developer-guides/execute-a-swap-with-the-aggregator-api.md) for examples of how to implement the swap.

**While both versions of the API remains backwards compatible, only the `[V2]` APIs will continue to receive updates and hence developers are highly encouraged to implement the latest `[V2]` APIs to avoid any disruptions as the `[V1]` API is eventually deprecated.**
{% endhint %}

{% swagger src="../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (3).yaml" path="/{chain}/route/encode" method="get" %}
[Kyber-Swap-Aggregator-APIs (3).yaml](<../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (3).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (3).yaml" path="/{chain}/api/v1/routes" method="get" %}
[Kyber-Swap-Aggregator-APIs (3).yaml](<../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (3).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (3).yaml" path="/{chain}/api/v1/route/build" method="post" %}
[Kyber-Swap-Aggregator-APIs (3).yaml](<../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (3).yaml>)
{% endswagger %}
