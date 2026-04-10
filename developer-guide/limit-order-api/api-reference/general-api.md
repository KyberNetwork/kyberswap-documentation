---
description: General endpoints for querying supported pairs and contract addresses.
---

# General API

## General

### Get Supported Pairs

`GET /read-partner/api/v1/orders/pairs`

Returns all token pairs for which active limit orders exist on the specified chain.

{% openapi-operation spec="limit-order" path="/read-partner/api/v1/orders/pairs" method="get" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

***

### Get Contract Address

`GET /read-ks/api/v1/configs/contract-address`

Returns the deployed Limit Order contract addresses for a given chain ID.

{% openapi-operation spec="limit-order" path="/read-ks/api/v1/configs/contract-address" method="get" %}
[OpenAPI limit-order](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/ff93b2af1088f794fbd0be8747eb18154a1641c007681d048eabba5cefaf6fd1.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260410%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260410T063451Z&X-Amz-Expires=172800&X-Amz-Signature=ba3f39f1d0f567aaaa1e937471008d9482a35cb8a9611214ab5fcbdf36461d1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% hint style="info" %}
The full return object is defined in the OpenAPI YAML. GitBook has limited support for `additionalProperties`, so refer to the YAML directly for the complete schema.
{% endhint %}

For a static list of deployed addresses, see [Contracts & Addresses.](../contracts-and-addresses.md)

