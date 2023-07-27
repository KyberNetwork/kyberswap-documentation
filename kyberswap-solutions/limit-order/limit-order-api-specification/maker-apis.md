---
description: KyberSwap Limit Order Maker APIs
---

# Maker APIs

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/Limit-Order-APIs (18).yaml" %}

## Maker APIs

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

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (1).yaml" path="/write/api/v1/orders" method="post" %}
[Limit-Order-APIs (1).yaml](<../../../.gitbook/assets/Limit-Order-APIs (1).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (26).yaml" path="/read-ks/api/v1/orders/active-making-amount" method="get" %}
[Limit-Order-APIs (26).yaml](<../../../.gitbook/assets/Limit-Order-APIs (26).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (3).yaml" path="/read-ks/api/v1/orders" method="get" %}
[Limit-Order-APIs (3).yaml](<../../../.gitbook/assets/Limit-Order-APIs (3).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (25).yaml" path="/write/api/v1/orders/sign-message" method="post" %}
[Limit-Order-APIs (25).yaml](<../../../.gitbook/assets/Limit-Order-APIs (25).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (13).yaml" path="/write/api/v1/encode/increase-nonce" method="post" %}
[Limit-Order-APIs (13).yaml](<../../../.gitbook/assets/Limit-Order-APIs (13).yaml>)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/Limit-Order-APIs (10).yaml" path="/write/api/v1/encode/cancel-batch-orders" method="post" %}
[Limit-Order-APIs (10).yaml](<../../../.gitbook/assets/Limit-Order-APIs (10).yaml>)
{% endswagger %}
