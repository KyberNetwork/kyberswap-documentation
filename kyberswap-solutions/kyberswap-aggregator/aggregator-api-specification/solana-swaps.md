---
description: KyberSwap Aggregator Solana APIs
---

# Solana Swaps

## Download OpenAPI specification:&#x20;

{% file src="../../../.gitbook/assets/Solana-Aggregator-APIs (11).yaml" %}

{% hint style="success" %}
#### Note on integrations: clientID

In order to continuously improve the KyberSwap Aggregator, our APIs implement a `clientData` or `source` field that enables us to understand how the APIs are being utilized. As a developer integrating with our APIs, **please add your clientID (i.e. company name) to the `clientData`/`source` fields** to enable us to serve you better.&#x20;

#### Example

* `[V1]GET`
  * clientData={"source":"yourCompanyNameHere"}
* `[V2]POST`
  * source="yourCompanyNameHere"
{% endhint %}

## Solana swap APIs

{% swagger src="../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml" path="/route" method="get" %}
[Solana-Aggregator-APIs (2).yaml](<../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml" path="/dexes" method="get" %}
[Solana-Aggregator-APIs (2).yaml](<../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml" path="/route/encode" method="get" %}
[Solana-Aggregator-APIs (2).yaml](<../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml>)
{% endswagger %}
