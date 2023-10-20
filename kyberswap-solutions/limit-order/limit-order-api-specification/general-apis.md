---
description: KyberSwap Limit Order General APIs
---

# General APIs

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" %}

## General APIs

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

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-partner/api/v1/orders/pairs" method="get" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml" path="/read-ks/api/v1/configs/contract-address" method="get" %}
[LimitOrderAPIs_v1.2.yaml](../../../.gitbook/assets/LimitOrderAPIs_v1.2.yaml)
{% endswagger %}

_\*For `/read-ks/api/v1/configs/contract-address`, please refer to the `.yaml` file for the full return object as GitBook has limited support for OpenAPI's `additionalProperties` definition._
