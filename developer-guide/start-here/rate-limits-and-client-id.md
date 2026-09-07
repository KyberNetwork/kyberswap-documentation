---
description: Note on integration
---

# Rate Limits & Authentication

Public rate limits are **3 rps** (requests per second) for the Aggregator API, **10 rps** for the Limit Order API, and **1 rps** for the ZaaS API.

## Aggregator API

The Aggregator API accepts two identification headers.

<table><thead><tr><th width="194.87890625">Header</th><th>Base URL</th></tr></thead><tbody><tr><td><code>X-Api-Key</code></td><td><code>https://api.kyberswap.com/swap/</code></td></tr><tr><td><code>x-client-id</code></td><td><code>https://aggregator-api.kyberswap.com</code></td></tr></tbody></table>

**Existing integrations**

Nothing changes. Clients are recommended to include the `x-client-id` header in every request, using your app or company name as the value.

* `GET` /routes — header `x-client-id: MyAwesomeApp`
* `POST` /route/build — header `x-client-id: MyAwesomeApp`

**New integrations and higher rate limits**

Request an API key and send it as an `X-Api-Key` header to the API gateway at `https://api.kyberswap.com/swap/`. The gateway provides better performance and higher rate limits.

* `GET` /routes — header `X-Api-Key: your-api-key`
* `POST` /route/build — header `X-Api-Key: your-api-key`

**Note:** client-id whitelisting is no longer offered for the Aggregator API. Rate limit increases are handled through API keys. To request one, contact the KyberSwap team at [business@kyber.network](mailto:business@kyber.network).

## Limit Order API and ZaaS API

These APIs do not require authentication, and API keys do not apply to them.

Include the `x-client-id` header in every request, using your app or company name as the value.

To get your client-id whitelisted and increase your rate limit, contact KyberSwap's team at [business@kyber.network](mailto:business@kyber.network).
