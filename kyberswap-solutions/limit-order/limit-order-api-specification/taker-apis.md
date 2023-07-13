---
description: KyberSwap Limit Order Taker APIs
---

# Taker APIs

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/Limit-Order-APIs (14).yaml" %}

## Taker APIs

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

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (7).yaml" path="/read-partner/api/v1/orders" method="get" %}
[Limit-Order-APIs (7).yaml](<../../../.gitbook/assets/Limit-Order-APIs (7).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (15).yaml" path="/read-partner/api/v1/encode/fill-order-to" method="post" %}
[Limit-Order-APIs (15).yaml](<../../../.gitbook/assets/Limit-Order-APIs (15).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (20).yaml" path="/read-partner/api/v1/encode/fill-batch-orders-to" method="post" %}
[Limit-Order-APIs (20).yaml](<../../../.gitbook/assets/Limit-Order-APIs (20).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (17).yaml" path="/read-partner/api/v1/orders/pairs" method="get" %}
[Limit-Order-APIs (17).yaml](<../../../.gitbook/assets/Limit-Order-APIs (17).yaml>)
{% endswagger %}
