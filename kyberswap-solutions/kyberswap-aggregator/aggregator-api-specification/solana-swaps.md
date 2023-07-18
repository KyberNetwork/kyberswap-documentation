---
description: KyberSwap Aggregator Solana APIs
---

# Solana Swaps

## Download OpenAPI specification:&#x20;

{% file src="../../../.gitbook/assets/Solana-Aggregator-APIs (11).yaml" %}

{% hint style="success" %}
#### Note on integrations: clientID

In order to continuously improve the KyberSwap Aggregator, our APIs implement a client identifier field that enables us to understand how the APIs are being utilized. As a developer integrating with our APIs, **please add your clientID (i.e. company name) to the `x-client-id` field in the API header** to enable us to serve you better.

For integrators who have previously specified your clientID under the `clientData`/`source` fields in the query params, we highly encourage using the `x-client-id` in the headers instead. As KyberSwap continues to optimize our Aggregator API,  support for reading clientID from the query params will be deprecated.

#### Example

* \[V1]`GET/POST` Header
  * x-client-id="yourCompanyNameHere"
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

## Solana swap APIs

### `Latest`

{% swagger src="../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml" path="/route" method="get" %}
[Solana-Aggregator-APIs (2).yaml](<../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml" path="/dexes" method="get" %}
[Solana-Aggregator-APIs (2).yaml](<../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml" path="/route/encode" method="get" %}
[Solana-Aggregator-APIs (2).yaml](<../../../.gitbook/assets/Solana-Aggregator-APIs (2).yaml>)
{% endswagger %}
