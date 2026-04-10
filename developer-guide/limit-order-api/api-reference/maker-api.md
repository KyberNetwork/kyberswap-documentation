---
description: Maker API endpoints for creating, querying, and cancelling limit orders.
---

# Maker API

## Maker

Maker endpoints handle the full lifecycle of a limit order from the Maker's perspective: creating orders gaslessly, querying their status, and cancelling them either gaslessly or on-chain.

For step-by-step integration guides, see:

* [Place a Limit Order](../how-to-guides/place-a-limit-order.md)
* [Cancel an Order — Gasless](../how-to-guides/cancel-an-order-gasless.md)
* [Cancel an Order — Hard Cancel](../how-to-guides/cancel-an-order-hard-cancel.md)

***

### Get Unsigned Create Order Message <a href="#get-unsigned-create-order-message" id="get-unsigned-create-order-message"></a>

`POST /write/api/v1/orders/sign-message`

Returns an unsigned EIP-712 typed data object that the Maker must sign before submitting an order. The `domain`, `types`, and `message` fields are passed directly to `signTypedData`.

{% openapi-operation spec="limit-order" path="/write/api/v1/orders/sign-message" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Create Order <a href="#create-order" id="create-order"></a>

`POST /write/api/v1/orders`

Submits a signed limit order to the KyberSwap orderbook. The request body is the unsigned order body extended with `salt` (from the sign-message response) and `signature` (from the Maker's wallet).

{% openapi-operation spec="limit-order" path="/write/api/v1/orders" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Get Maker Orders <a href="#get-maker-orders" id="get-maker-orders"></a>

`GET /read-ks/api/v1/orders`

Returns all orders for a Maker address, filterable by status (`active`, `open`, `cancelled`, `filled`, `expired`).

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/orders" method="get" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Get Active Making Amount <a href="#get-active-making-amount" id="get-active-making-amount"></a>

`GET /read-ks/api/v1/orders/active-making-amount`

Returns the total `makingAmount` currently committed across all open orders for a Maker and token. Use this before creating a new order to determine the total allowance required.

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/orders/active-making-amount" method="get" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Get Unsigned Cancel Message <a href="#get-unsigned-cancel-message" id="get-unsigned-cancel-message"></a>

`POST /write/api/v1/orders/cancel-sign`

Returns an unsigned EIP-712 cancel message for one or more `orderIds`. Sign the returned message and pass it to `POST /write/api/v1/orders/cancel`.

{% openapi-operation spec="limit-order" path="/write/api/v1/orders/cancel-sign" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Gasless Cancel Order <a href="#gasless-cancel-order" id="gasless-cancel-order"></a>

`POST /write/api/v1/orders/cancel`

Submits a signed gasless cancel request. The KyberSwap Operator will stop co-signing the specified orders. If the Operator recently signed an order, cancellation may take up to 5 minutes.

Requires the `Origin` header to be set.

{% openapi-operation spec="limit-order" path="/write/api/v1/orders/cancel" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Encode Hard Cancel <a href="#encode-hard-cancel" id="encode-hard-cancel"></a>

`POST /read-ks/api/v1/encode/cancel-batch-orders`

Returns encoded calldata to cancel one or more specific orders on-chain. Multiple `orderIds` can be batched into a single transaction. The caller pays gas but the cancellation is immediate.

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/encode/cancel-batch-orders" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Encode Increase Nonce <a href="#encode-increase-nonce" id="encode-increase-nonce"></a>

`POST /read-ks/api/v1/encode/increase-nonce`

Returns encoded calldata to increment the Maker's nonce in the Limit Order contract, which immediately invalidates **all** open orders. Use when you want to cancel everything at once.

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/encode/increase-nonce" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
