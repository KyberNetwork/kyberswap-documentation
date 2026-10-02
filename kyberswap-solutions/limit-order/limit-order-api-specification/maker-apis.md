---
description: KyberSwap Limit Order Maker APIs
---

# Maker APIs

## Download OpenAPI specification:

{% file src="../../../.gitbook/assets/LimitOrderAPIs_v1.3 (1).yaml" %}

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

{% openapi-operation spec="limit-order" path="/write/api/v1/orders/sign-message" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/dbbbe0a0e397675884e9a3e19597800fdad21fcd2201ea03cf8d9243b6723c30.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20261002%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261002T082124Z&X-Amz-Expires=172800&X-Amz-Signature=45ec4966aed41aef114aad41a6483541fb4a157ab5f0ff89dff29a18b215b84a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="limit-order" path="/write/api/v1/orders" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/dbbbe0a0e397675884e9a3e19597800fdad21fcd2201ea03cf8d9243b6723c30.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20261002%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261002T082124Z&X-Amz-Expires=172800&X-Amz-Signature=45ec4966aed41aef114aad41a6483541fb4a157ab5f0ff89dff29a18b215b84a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

#### Query Maker Order(s)

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/orders" method="get" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/dbbbe0a0e397675884e9a3e19597800fdad21fcd2201ea03cf8d9243b6723c30.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20261002%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261002T082124Z&X-Amz-Expires=172800&X-Amz-Signature=45ec4966aed41aef114aad41a6483541fb4a157ab5f0ff89dff29a18b215b84a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/orders/active-making-amount" method="get" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/dbbbe0a0e397675884e9a3e19597800fdad21fcd2201ea03cf8d9243b6723c30.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20261002%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261002T082124Z&X-Amz-Expires=172800&X-Amz-Signature=45ec4966aed41aef114aad41a6483541fb4a157ab5f0ff89dff29a18b215b84a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

#### Gasless Cancel Order(s)

{% hint style="success" %}
**Developer Guide**

Please refer to [**Gasless Cancel**](../developer-guides/gasless-cancel.md) for the relevant sequence diagram as well as a TypeScript example.
{% endhint %}

{% openapi-operation spec="limit-order" path="/write/api/v1/orders/cancel-sign" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/dbbbe0a0e397675884e9a3e19597800fdad21fcd2201ea03cf8d9243b6723c30.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20261002%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261002T082124Z&X-Amz-Expires=172800&X-Amz-Signature=45ec4966aed41aef114aad41a6483541fb4a157ab5f0ff89dff29a18b215b84a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="limit-order" path="/write/api/v1/orders/cancel" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/dbbbe0a0e397675884e9a3e19597800fdad21fcd2201ea03cf8d9243b6723c30.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20261002%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261002T082124Z&X-Amz-Expires=172800&X-Amz-Signature=45ec4966aed41aef114aad41a6483541fb4a157ab5f0ff89dff29a18b215b84a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

#### Hard Cancel Order(s)

{% hint style="success" %}
**Developer Guide**

Please refer to [**Hard Cancel**](../developer-guides/hard-cancel.md) for the relevant sequence diagram as well as a TypeScript example.
{% endhint %}

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/encode/cancel-batch-orders" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/dbbbe0a0e397675884e9a3e19597800fdad21fcd2201ea03cf8d9243b6723c30.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20261002%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261002T082124Z&X-Amz-Expires=172800&X-Amz-Signature=45ec4966aed41aef114aad41a6483541fb4a157ab5f0ff89dff29a18b215b84a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/encode/increase-nonce" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/dbbbe0a0e397675884e9a3e19597800fdad21fcd2201ea03cf8d9243b6723c30.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20261002%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261002T082124Z&X-Amz-Expires=172800&X-Amz-Signature=45ec4966aed41aef114aad41a6483541fb4a157ab5f0ff89dff29a18b215b84a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
