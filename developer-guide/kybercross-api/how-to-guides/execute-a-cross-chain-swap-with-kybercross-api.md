---
description: Interacting with KyberCross through the KyberCross API
---

# Execute A Cross-Chain Swap With KyberCross API

## Overview

{% hint style="info" %}
**Disclaimer: Data provided as-is.** The route plans and transaction calldata returned by the KyberCross API are provided as-is. You are responsible for verifying each transaction before you submit it, and for any losses that result from it.
{% endhint %}

The KyberCross API is a public API for quoting a cross-chain route, building one source-chain transaction, and tracking execution. For every endpoint, parameter and response, see API Reference.

Get a built source transaction either by:

* Separate path: `POST /api/v1/quotes`, choose a `route_plan`, then pass that plan unchanged to `POST /api/v1/builds`; or
* Combined path: `POST /api/v1/quote-and-build`.

The guide below follows the separate path.

{% hint style="info" %}
**Combined path**

`POST /api/v1/quote-and-build` quotes routes, then builds the best plan in one call. `all_route_plans` is ignored. Build validation matches `/api/v1/builds`. Submit `data.build.tx`. For ERC-20 source input, check allowance against `data.build.tx.to` and approve only if needed.
{% endhint %}

### TypeScript Example

The snippets below use `fetch` and [ethers.js](https://docs.ethers.org/). Values come from the request examples in the API Reference. Send header `x-api-key` on every request; see the API key note in the API Reference.

```typescript
const BASE_URL = "https://api.kyberswap.com/crosschain-swap";
const headers = {
  "x-api-key": process.env.KYBERCROSS_API_KEY!,
  "Content-Type": "application/json",
};
```

Discover with `GET /api/v1/supported-networks` and `GET /api/v1/bridge-providers`. Supported networks are returned as `name` and numeric `chain_id`.

#### Step 1: Query Cross-Chain Routes

```typescript
const quoteRequest = {
  from_chain: "ethereum",
  from_token: "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
  from_token_decimals: 6,
  from_address: "0x1111111111111111111111111111111111111111",
  to_chain: "base",
  to_token: "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913",
  to_token_decimals: 6,
  to_address: "0x1111111111111111111111111111111111111111",
  amount: "1000000",
  slippage_bps: 50,
};

const quote = await fetch(`${BASE_URL}/api/v1/quotes`, {
  method: "POST",
  headers,
  body: JSON.stringify(quoteRequest),
}).then((res) => res.json());

const routePlan = quote.data.route_plans[0];
const spender = quote.data.ks_allowance_hub_address;
```

Amounts are decimal integer strings in token base units. Native token uses sentinel `0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE`.

The response contains:

* `route_plans`: Route plans sorted best-first. Holds exactly one item (the best plan) unless `all_route_plans` was true in the request.
* `ks_allowance_hub_address`: Source-chain ERC-20 allowance spender for the separate quote/build path. Same address as build response `data.tx.to`. Check allowance and approve only if needed for ERC-20 source input.

Each route plan carries `tags`: `RECOMMENDED` is the first ranked returned plan; `FASTEST` has the lowest `estimated_duration_sec`; `BEST_OUTPUT` has the highest `expected_output_amount`.

For the full list of request fields, including `include_bridges`, `exclude_bridges`, `partner_fee_bps` and `gas_drop`, see **Quote routes** in the API Reference.

#### Step 2: Build The Source Transaction

```typescript
const build = await fetch(`${BASE_URL}/api/v1/builds`, {
  method: "POST",
  headers,
  body: JSON.stringify(routePlan),
}).then((res) => res.json());

const tx = build.data.tx;
```

Builds one source-chain transaction from a route plan returned by `/api/v1/quotes` or `/api/v1/quote-and-build`. Pass the plan through unchanged, including opaque fields.

Opaque route-plan fields (`sig`, `bridge.metadata`, swap `metadata`, `dest_intent`) are server-issued. Copy them unchanged; do not construct, strip, or reinterpret them. If a plan is rejected as invalid or expired, request a new quote.

The built transaction is returned under `data.tx` with `to`, `data` (hex-encoded calldata), `value` and `gas`.

#### Step 3: Approve The Source Token (ERC-20 Only)

```typescript
import { Contract } from "ethers";

const erc20 = new Contract(
  quoteRequest.from_token,
  [
    "function allowance(address owner, address spender) view returns (uint256)",
    "function approve(address spender, uint256 amount) returns (bool)",
  ],
  signer,
);

const allowance = await erc20.allowance(quoteRequest.from_address, spender);
if (allowance < BigInt(quoteRequest.amount)) {
  await (await erc20.approve(spender, quoteRequest.amount)).wait();
}
```

For ERC-20 source input only, check allowance against the build spender and approve if needed. The separate path spender is the quote response `data.ks_allowance_hub_address` (same address as build response `data.tx.to`). Native source input needs no ERC-20 approval.

#### Step 4: Execute The Source Transaction On-Chain

```typescript
const sent = await signer.sendTransaction({
  to: tx.to,
  data: tx.data,
  value: BigInt(tx.value),
  gasLimit: tx.gas ? BigInt(tx.gas) : undefined,
});

const sourceTxHash = sent.hash;
```

Submit the built source transaction from build response `data.tx`. The source transaction hash is used to track the execution.

#### Step 5: Track The Execution

```typescript
const execution = await fetch(
  `${BASE_URL}/api/v1/executions?source_tx_hash=${sourceTxHash}`,
  { headers },
).then((res) => res.json());

const { route_state, fund_state, gas_drop_state } = execution.data.route_execution;
```

Poll `GET /api/v1/executions` with the source transaction hash. It returns the public tracking record for a submitted source transaction.

* `route_state`: Route lifecycle. Terminal values: `SUCCESS`, `REFUNDED`, `FAILED`.
* `fund_state`: Where funds currently sit on the route.
* `gas_drop_state`: Optional gas-drop lifecycle for a route execution. `null` means no planned gas drop.

For all states and execution details, see **Get route execution by source transaction hash** in the [API Reference](../api-reference.md).

{% hint style="info" %}
**Withdraw a failed execution**

If an execution is exactly `FAILED` / `UNRECOVERED`, the owner may call `POST /api/v1/executions/{source_tx_hash}/withdrawals/build`, then submit the returned `data.tx` on the destination chain as `data.owner`. See **Build owner withdrawal transaction** in the [API Reference](../api-reference.md).
{% endhint %}
