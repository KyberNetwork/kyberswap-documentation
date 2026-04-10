---
description: Note on integration
---

# Rate Limits & Client ID

KyberSwap APIs do not require authentication. There are no API keys, tokens, or secrets. However, all APIs support an optional client identifier header that affects your rate limit tier.

Clients are recommended to include the `x-client-id` header in every request, using your app or company name as the value.

* **\[V1] Get Swap Route**
  * **Header:** `x-client-id`
* **\[V1] Post Swap Route For Encoded Data**
  * **Header:** `x-client-id`

For example:

* \[V1] `GET` /routes
  * Header
    * `x-client-id: MyAwesomeApp`
* \[V1] `POST` /route/build
  * Header
    * `x-client-id: MyAwesomeApp`

This will enable us to serve you better as we continuously strive to improve our API.&#x20;



### Requesting a Higher Limit

By default, the Aggregator API allows **3 rps** (requests per second), and the ZaaS API allows **1 rps.**

If you wish to get your client-id whitelisted and to increase the rate limit, contact the KyberSwap BD team at [**business@kyber.network**](mailto:business@kyber.network)**.**
