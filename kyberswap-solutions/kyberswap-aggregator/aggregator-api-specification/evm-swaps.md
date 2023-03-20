---
description: KyberSwap Aggregator EVM APIs
---

# EVM Swaps

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs.yaml" %}

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

{% swagger src="../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (14).yaml" path="/{chain}/route/encode" method="get" %}
[Kyber-Swap-Aggregator-APIs (14).yaml](<../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (14).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (14).yaml" path="/{chain}/api/v1/routes" method="get" %}
[Kyber-Swap-Aggregator-APIs (14).yaml](<../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs (14).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs.yaml" path="/{chain}/api/v1/route/build" method="post" %}
[Kyber-Swap-Aggregator-APIs.yaml](../../../.gitbook/assets/Kyber-Swap-Aggregator-APIs.yaml)
{% endswagger %}
