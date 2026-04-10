---
description: >-
  Use the ZaaS API to migrate an existing liquidity position from one pool to  
  another in a single transaction.
---

# Zap Migrate — Move Between Pools

## Zap Migrate — Move Between Pools

Zap Migrate lets users move their liquidity from a source pool (or position) to a destination pool without manually removing liquidity, swapping, and re-depositing. This is useful for rebalancing across DEXes, fee tiers, or price ranges.

### Prerequisites

* Know the source position (`positionId` or tick range + pool) to migrate from.
* Know the destination pool and target tick range.
* Approve the `KSZapRouterPosition` contract on the source token if required.

{% hint style="info" %}
Curve and Balancer pools can be used as the **source** of a migration but not as the destination. See Supported Chains & DEXes.
{% endhint %}

### Flow Overview

```
GetMigrateRoute  →  (user reviews preview)  →  BuildMigrateRoute  →  send transaction
```

### Step 1 — Preview the Migrate Route

Call `GET /api/v1/migrate/route` to preview the migration before the user confirms.

**Key request parameters:**

| Parameter                          | Description                                                      |
| ---------------------------------- | ---------------------------------------------------------------- |
| `dexFrom`                          | Source DEX ID — see [DEX IDs](../zaps-supported-chains-dexes.md) |
| `dexTo`                            | Destination DEX ID                                               |
| `poolFrom.id`                      | Source pool address                                              |
| `poolTo.id`                        | Destination pool address                                         |
| `position.id`                      | Source position NFT ID                                           |
| `position.tickLower` / `tickUpper` | Target tick range in the destination pool                        |
| `slippage`                         | Slippage tolerance in basis points                               |

**Key response fields:**

| Field                    | Description                                    |
| ------------------------ | ---------------------------------------------- |
| `poolDetails`            | Pool info after zapping for destination pools  |
| `positionDetails`        | Estimated new position in the destination pool |
| `zapDetails.priceImpact` | Combined price impact of the migration         |
| `route`                  | Encoded route to pass to `BuildMigrateRoute`   |

### Step 2 — Build the Transaction

Call `POST /api/v1/migrate/route/build` with the `route` from Step 1:

```bash
curl -X POST "https://zap-api.kyberswap.com/{chain}/api/v1/migrate/route/build" \
-H "content-type: application/json" \
-H "x-client-id: your-client-id" \
-d '{
  "sender": "0xYourAddress",
  "recipient": "0xYourAddress",
  "route": "<route from GetMigrateRoute response>",
  "deadline": 1800000000
}'
```

### Step 3 — Send the Transaction

```javascript
const tx = await signer.sendTransaction({
  to:    buildResponse.routerAddress,
  data:  buildResponse.calldata,
  value: buildResponse.value,
  gasLimit: getMigrateRouteResponse.gas * 2,
});
```
