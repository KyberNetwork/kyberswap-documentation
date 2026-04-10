---
description: >-
  Use the ZaaS API to open a new concentrated liquidity position or increase
  an   existing one using any input token.
---

# Zap In - Enter a Liquidity Position

## Zap In — Enter a Liquidity Position

Zap In lets users deposit any ERC-20 or native token into a concentrated liquidity position. The API handles the swap into the correct token ratio and the liquidity mint in a single on-chain transaction.

### Prerequisites

* Know the target pool (`pool.id`) and position tick range (`tickLower`, `tickUpper`), or an existing `positionId` to increase.
* Have the input token address and amount ready.
* Approve the `KSZapRouterPosition` contract to spend the input token (or use the permit flow for EIP-2612 tokens).

### Flow Overview

```
GetRoute  →  (user reviews preview)  →  BuildRoute  →  send transaction
```

### Step 1 — Preview the Route

Call `GET /api/v1/in/route` to get a route preview before asking the user to confirm.

**Example request (new position on Uniswap V3, Polygon):**

```bash
curl -X GET "https://zap-api.kyberswap.com/polygon/api/v1/in/route\
?dex=DEX_UNISWAPV3\
&pool.id=0xb46388f104ff88aac68626a316aaf3a924f32055\
&position.tickLower=-24800\
&position.tickUpper=32400\
&tokensIn=0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE\
&amountsIn=1000000000000000000\
&slippage=100" \
-H "x-client-id: your-client-id"
```

**Key request parameters:**

| Parameter                          | Description                                               |
| ---------------------------------- | --------------------------------------------------------- |
| `dex`                              | DEX ID — see [DEX IDs](../zaps-supported-chains-dexes.md) |
| `pool.id`                          | Pool contract address                                     |
| `position.tickLower` / `tickUpper` | Price range for a new position                            |
| `position.id`                      | Existing position NFT ID (for increasing liquidity)       |
| `tokensIn`                         | Input token address (comma-separated for multiple)        |
| `amountsIn`                        | Token amount in raw units, no decimals (comma-separated)  |
| `slippage`                         | Slippage tolerance in basis points (e.g. `100` = 1%)      |

**Key response fields to surface to users:**

| Field                        | What to show                                                                  |
| ---------------------------- | ----------------------------------------------------------------------------- |
| `poolDetails`                | Pool state after zapping, warn if pool price deviates significantly after zap |
| `positionDetails`            | Previewed position range and estimated liquidity                              |
| `zapDetails.priceImpact`     | Show price impact warning if high                                             |
| `zapDetails.remainingAmount` | Any leftover tokens returned to the user                                      |
| `routerAddress`              | Use for allowance check before building                                       |

{% hint style="warning" %}
Show users the price impact and pool price deviation. A large deviation means the position may be subject to immediate arbitrage.
{% endhint %}

### Step 2 — Build the Transaction

Once the user confirms, call `POST /api/v1/in/route/build` with the `route` value from Step 1:

```bash
curl -X POST "https://zap-api.kyberswap.com/polygon/api/v1/in/route/build" \
-H "content-type: application/json" \
-H "x-client-id: your-client-id" \
-d '{
  "sender": "0xYourAddress",
  "recipient": "0xYourAddress",
  "route": "<route from GetRoute response>",
  "deadline": 1800000000
}'
```

### Step 3 — Send the Transaction

Use the `calldata`, `value` (for native token), and `routerAddress` from the build response to submit the transaction with your web3 library.

```javascript
const tx = await signer.sendTransaction({
  to:    buildResponse.routerAddress,
  data:  buildResponse.calldata,
  value: buildResponse.value,       // only non-zero for native token input
  gasLimit: getRouteResponse.gas * 2,  // use 2–2.5x the estimated gas
});
```
