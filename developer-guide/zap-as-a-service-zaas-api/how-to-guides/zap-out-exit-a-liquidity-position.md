---
description: >-
  Use the ZaaS API to remove liquidity from a concentrated liquidity position  
  and receive a single output token.
---

# Zap Out — Exit a Liquidity Position

## Zap Out — Exit a Liquidity Position

Zap Out lets users exit a liquidity position and receive their value as a single token of their choice — no manual removal, swapping, or combining of two tokens required.

### Prerequisites

* Know the position NFT ID (`positionId`) to exit.
* Know the desired output token address.
* The user must own (or be approved to act on) the position NFT.

### Flow Overview

```
GetOutRoute  →  (user reviews preview)  →  BuildOutRoute  →  send transaction
```

### Step 1 — Preview the Zap-Out Route

Call `GET /api/v1/out/route` to preview how much the user will receive.

**Key request parameters:**

| Parameter     | Description                                                                                                   |
| ------------- | ------------------------------------------------------------------------------------------------------------- |
| `dex`         | DEX ID of the source pool — see [DEX IDs](../../../kyberswap-solutions/kyberswap-zap-as-a-service/dex-ids.md) |
| `pool.id`     | Pool contract address                                                                                         |
| `position.id` | Position NFT ID to exit                                                                                       |
| `tokenOut`    | Desired output token address                                                                                  |
| `slippage`    | Slippage tolerance in basis points (e.g. `100` = 1%)                                                          |

**Key response fields to surface to users:**

| Field                    | Description                                     |
| ------------------------ | ----------------------------------------------- |
| `zapDetails.amountOut`   | Estimated output amount after fees and swap     |
| `zapDetails.priceImpact` | Price impact of the exit swap                   |
| `zapDetails.fees`        | Protocol and partner fees deducted              |
| `route`                  | Encoded route to pass to `BuildOutRoute`        |
| `routerAddress`          | Router contract; user must approve NFT transfer |

### Step 2 — Build the Transaction

Call `POST /api/v1/out/route/build` with the `route` from Step 1:

```bash
curl -X POST "https://zap-api.kyberswap.com/{chain}/api/v1/out/route/build" \
-H "content-type: application/json" \
-H "x-client-id: your-client-id" \
-d '{
  "sender": "0xYourAddress",
  "recipient": "0xYourAddress",
  "route": "<route from GetOutRoute response>",
  "deadline": 1800000000
}'
```

### Step 3 — Send the Transaction

```javascript
const tx = await signer.sendTransaction({
  to:    buildResponse.routerAddress,
  data:  buildResponse.calldata,
  value: buildResponse.value,
  gasLimit: getOutRouteResponse.gas * 2,
});
```

{% hint style="info" %}
Set `gasLimit` to **2–2.5× the estimated gas** from the `GetOutRoute` response.
{% endhint %}
