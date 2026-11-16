---
description: Integrate cross-chain swaps with the KyberCross API
---

# KyberCross API

## Overview

KyberCross is KyberSwap's cross-chain swap technology, built with KyberSwap Aggregator at its core. With the KyberCross API, you can bring cross-chain swaps into your application: quote a cross-chain route, build one source-chain transaction for your user to submit, and track the execution until it completes.

{% hint style="info" %}
**Disclaimer: Data provided as-is.** The KyberCross API returns route plans and transaction calldata as-is. Integrators are responsible for verifying the transactions they submit.
{% endhint %}

{% hint style="info" %}
**Note on integration: API key**

Requests without an API key are rate-limited to 10 requests per 10 seconds.&#x20;

To request an API key for a higher rate limit, contact the Business Development team at [business@kyber.network](mailto:business@kyber.network). Once you have a key, send it in the `x-api-key` header on every request, including the discovery endpoints.
{% endhint %}

### Why integrate the KyberCross API

* **Aggregator routing on both chains:** swap legs on the source and destination chains are routed by KyberSwap Aggregator.
* **One transaction for your users:** the API builds one source-chain transaction. The destination-side action is carried out through the destination intent included in the route plan.
* **Multiple bridge providers:** routes are quoted across KyberCross's bridge providers. Use `include_bridges` or `exclude_bridges` to control which providers are considered.
* **Choose by output or speed:** each quote labels its plans as `RECOMMENDED`, `FASTEST` and `BEST_OUTPUT`. Set `all_route_plans` to `true` for every built plan, sorted best-first.
* **Partner fee:** charge a partner fee on each route with `partner_fee_bps` and `partner_fee_recipient`.
* **Gas on arrival:** set `gas_drop=true` to include a destination native gas drop before the main destination action.
* **Tracking and recovery:** follow each execution by its source transaction hash, with `route_state`, `fund_state` and `gas_drop_state`. If an execution is exactly `FAILED` / `UNRECOVERED`, the owner can build a withdrawal transaction on the destination chain.

### How a KyberCross route works

1. **Source swap (`source_swap`):** KyberSwap Aggregator swaps the input token into a bridge token on the source chain.
2. **Bridge (`bridge`):** KyberCross compares quotes from its bridge providers and uses the selected provider to move the bridge token to the destination chain.
3. **Destination swap (`dest_swap`):** KyberSwap Aggregator swaps the bridge token into the output token on the destination chain.

A route plan's `flow_type` is one of `bridge_only`, `swap_then_bridge`, `bridge_then_swap` or `swap_bridge_swap`. `bridge_then_swap` and `swap_bridge_swap` always include a destination intent; `bridge_only` and `swap_then_bridge` include one when `gas_drop=true`. When requested, a gas-drop swap leg (`gas_drop_swap`) is also included.

### Supported networks and bridge providers

|                                     | Values in API spec v1.1.2                                                                                            |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Networks (`ChainName`)              | `ethereum`, `arbitrum`, `base`, `bsc`, `robinhood`, `hyperevm`, `elysium`                                            |
| Bridge providers (`BridgeProvider`) | `across`, `mayan`, `near_intents`, `relay`, `cctp_v2_fast`, `cctp_v2`, `ccip`, `eco`, `symbiosis`, `arbitrum_bridge` |

The live lists are returned by `GET /api/v1/supported-networks` and `GET /api/v1/bridge-providers`. Use these endpoints at runtime instead of hardcoding the values.
