---
description: KyberSwap Limit Order Maker APIs
---

# Maker APIs

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" %}

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

#### Create Order(s)

{% hint style="success" %}
**Developer Guide**

Please refer to [**Create Limit Order** ](../developer-guides/create-limit-order.md)for the relevant sequence diagram as well as a TypeScript example.
{% endhint %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/write/api/v1/orders/sign-message" method="post" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/write/api/v1/orders" method="post" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

#### Query Maker Order(s)

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-ks/api/v1/orders" method="get" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-ks/api/v1/orders/active-making-amount" method="get" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

#### Gasless Cancel Order(s)

{% hint style="success" %}
**Developer Guide**

Please refer to [**Gasless Cancel**](../developer-guides/gasless-cancel.md) for the relevant sequence diagram as well as a TypeScript example.
{% endhint %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/write/api/v1/orders/cancel-sign" method="post" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/write/api/v1/orders/cancel" method="post" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

#### Hard Cancel Order(s)

{% hint style="success" %}
**Developer Guide**

Please refer to [**Hard Cancel**](../developer-guides/hard-cancel.md) for the relevant sequence diagram as well as a TypeScript example.
{% endhint %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-ks/api/v1/encode/cancel-batch-orders" method="post" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-ks/api/v1/encode/increase-nonce" method="post" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}
