---
description: Endpoints, request and response schemas for the KyberCross API
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# API Reference

{% hint style="info" %}
Note on integration: API key

Send header `x-api-key` on every request, including discovery endpoints `GET /api/v1/supported-networks` and `GET /api/v1/bridge-providers`. The default rate limit is 10 requests per 10 seconds. To request an API key or a higher rate limit, contact the Business Development team at [business@kyber.network](mailto:business@kyber.network).
{% endhint %}

{% openapi-operation spec="kybercross" path="/api/v1/supported-networks" method="get" %}
[OpenAPI kybercross](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/cb1164d556a4457c5b33e5577a92f78c90d584cc871f8db11dc400bb7a98fa67.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=0cc7c3f440ca5fd44ab53362d4a69dfe%2F20261116%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261116T104542Z&X-Amz-Expires=172800&X-Amz-Signature=49393b634479bcb95ad29bff018cfd98cd592a8c48f2b76102909e6573b306f6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="kybercross" path="/api/v1/bridge-providers" method="get" %}
[OpenAPI kybercross](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/cb1164d556a4457c5b33e5577a92f78c90d584cc871f8db11dc400bb7a98fa67.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=0cc7c3f440ca5fd44ab53362d4a69dfe%2F20261116%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261116T104542Z&X-Amz-Expires=172800&X-Amz-Signature=49393b634479bcb95ad29bff018cfd98cd592a8c48f2b76102909e6573b306f6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="kybercross" path="/api/v1/quotes" method="post" %}
[OpenAPI kybercross](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/cb1164d556a4457c5b33e5577a92f78c90d584cc871f8db11dc400bb7a98fa67.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=0cc7c3f440ca5fd44ab53362d4a69dfe%2F20261116%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261116T104542Z&X-Amz-Expires=172800&X-Amz-Signature=49393b634479bcb95ad29bff018cfd98cd592a8c48f2b76102909e6573b306f6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="kybercross" path="/api/v1/builds" method="post" %}
[OpenAPI kybercross](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/cb1164d556a4457c5b33e5577a92f78c90d584cc871f8db11dc400bb7a98fa67.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=0cc7c3f440ca5fd44ab53362d4a69dfe%2F20261116%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261116T104542Z&X-Amz-Expires=172800&X-Amz-Signature=49393b634479bcb95ad29bff018cfd98cd592a8c48f2b76102909e6573b306f6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="kybercross" path="/api/v1/quote-and-build" method="post" %}
[OpenAPI kybercross](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/cb1164d556a4457c5b33e5577a92f78c90d584cc871f8db11dc400bb7a98fa67.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=0cc7c3f440ca5fd44ab53362d4a69dfe%2F20261116%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261116T104542Z&X-Amz-Expires=172800&X-Amz-Signature=49393b634479bcb95ad29bff018cfd98cd592a8c48f2b76102909e6573b306f6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="kybercross" path="/api/v1/executions" method="get" %}
[OpenAPI kybercross](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/cb1164d556a4457c5b33e5577a92f78c90d584cc871f8db11dc400bb7a98fa67.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=0cc7c3f440ca5fd44ab53362d4a69dfe%2F20261116%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261116T104542Z&X-Amz-Expires=172800&X-Amz-Signature=49393b634479bcb95ad29bff018cfd98cd592a8c48f2b76102909e6573b306f6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="kybercross" path="/api/v1/executions/{source_tx_hash}/withdrawals/build" method="post" %}
[OpenAPI kybercross](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/cb1164d556a4457c5b33e5577a92f78c90d584cc871f8db11dc400bb7a98fa67.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=0cc7c3f440ca5fd44ab53362d4a69dfe%2F20261116%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261116T104542Z&X-Amz-Expires=172800&X-Amz-Signature=49393b634479bcb95ad29bff018cfd98cd592a8c48f2b76102909e6573b306f6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
