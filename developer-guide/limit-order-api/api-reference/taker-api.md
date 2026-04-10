# Taker API

## Taker

Taker endpoints cover the full fill flow: query open orders sorted by best rate, obtain the required Operator co-signature, encode the fill calldata, and execute on-chain.

For a step-by-step guide, see [Fill a Limit Order](../../../kyberswap-solutions/limit-order/developer-guides/fill-limit-order.md).

For taker protocol fees and the rate calculation formula, see [Fee Structure.](../fee-structure.md)

***

### Get Open Orders <a href="#get-open-orders" id="get-open-orders"></a>

`GET /read-partner/api/v1/orders`

Returns open orders for a token pair sorted by best effective rate (descending). The rate accounts for partial fills and protocol fees — see Fee Structure.

{% openapi-operation spec="limit-order" path="/read-partner/api/v1/orders" method="get" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Get Operator Signature <a href="#get-operator-signature" id="get-operator-signature"></a>

`GET /read-partner/api/v1/orders/operator-signature`

Returns the KyberSwap Operator co-signature for one or more orders. This signature is required as part of the fill calldata and is short-lived — fetch it immediately before building the fill transaction.

{% openapi-operation spec="limit-order" path="/read-partner/api/v1/orders/operator-signature" method="get" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Encode Fill Order <a href="#encode-fill-order" id="encode-fill-order"></a>

`POST /read-ks/api/v1/encode/fill-order-to`

Returns encoded calldata to fill a **single** order on-chain. The encoded data is sent as `data` in the transaction to the Limit Order contract.

| Field               | Description                                                             |
| ------------------- | ----------------------------------------------------------------------- |
| `orderId`           | The order to fill                                                       |
| `takingAmount`      | Amount of `takerAsset` to provide (can be partial)                      |
| `thresholdAmount`   | Minimum `makingAmount` to receive — reverts if not met (slippage guard) |
| `target`            | Address to receive the `makerAsset`                                     |
| `operatorSignature` | From `GET /read-partner/api/v1/orders/operator-signature`               |

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/encode/fill-order-to" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Encode Fill Batch Orders <a href="#encode-fill-batch-orders" id="encode-fill-batch-orders"></a>

`POST /read-ks/api/v1/encode/fill-batch-orders-to`

Returns encoded calldata to fill **multiple** orders in a single on-chain transaction. The `orderIds` array and `operatorSignatures` array must be in the same order.

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/encode/fill-batch-orders-to" method="post" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
