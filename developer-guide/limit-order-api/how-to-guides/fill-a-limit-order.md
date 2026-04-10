---
description: >-
  Discover open limit orders and execute a fill on-chain as a Taker using the  
  KyberSwap Limit Order API.
---

# Fill a Limit Order

## Fill a Limit Order

Takers fill limit orders on-chain, earning the spread between the order rate and the current market rate. Every fill requires a KyberSwap Operator co-signature that authorises the specific fill — this prevents stale or frontrun fills.

{% hint style="success" %}
**Full demo:** [github.com/KyberNetwork/ks-limit-order-API-demo](https://github.com/KyberNetwork/ks-limit-order-API-demo)
{% endhint %}

### Flow

```
GET /orders  →  GET /operator-signature  →  check allowance
    →  POST /encode/fill-order-to  →  send transaction
```

### Step 1 — Get Open Orders

Query open orders for a token pair, sorted by best rate (descending):

```typescript
const { data } = await axios.get(
    "https://limit-order.kyberswap.com/read-partner/api/v1/orders",
    {
        params: {
            chainId: 137,
            makerAsset: "0x2791bca1...",   // token the Maker is selling
            takerAsset: "0x1C954E8f...",   // token the Taker must provide
        }
    }
);

const orders = data.data;   // sorted best-rate first
const targetOrderId = orders[0].id;
```

{% hint style="info" %}
Orders are sorted by the effective rate formula which accounts for partial fills and fees.
{% endhint %}

### Step 2 — Get the Operator Signature

The Operator signature is required for every fill. It is short-lived and must be fetched immediately before building the transaction:

```typescript
const { data: sigData } = await axios.get(
    "https://limit-order.kyberswap.com/read-partner/api/v1/orders/operator-signature",
    { params: { chainId: 137, orderIds: targetOrderId } }
);

const operatorSignature = sigData.data[0].operatorSignature;
```

### Step 3 — Check and Set Allowance

The Limit Order contract must be approved to spend the Taker's `takerAsset`:

```typescript
const takingAmount = BigInt(orders[0].takingAmount) / 2n;  // fill half the order

const allowance = await tokenContract.allowance(signerAddress, limitOrderContract);
if (allowance < takingAmount) {
    const tx = await tokenContract.approve(limitOrderContract, takingAmount);
    await tx.wait();
}
```

### Step 4 — Encode the Fill Calldata

```typescript
const requestBody = {
    orderId: Number(targetOrderId),
    takingAmount: takingAmount.toString(),
    thresholdAmount: "0",          // minimum makingAmount to receive (slippage guard)
    target: signerAddress,         // address to receive the makerAsset
    operatorSignature: operatorSignature
};

const { data: encoded } = await axios.post(
    "https://limit-order.kyberswap.com/read-ks/api/v1/encode/fill-order-to",
    requestBody
);
```

{% hint style="info" %}
**Batch fills:** Use `POST /read-ks/api/v1/encode/fill-batch-orders-to` to fill multiple orders in one transaction. Pass arrays of `orderIds` and `operatorSignatures` in matching order. See Fill Batch Orders.
{% endhint %}

### Step 5 — Execute On-chain

```typescript
const tx = await signer.sendTransaction({
    to:    limitOrderContract,
    from:  signerAddress,
    data:  encoded.data.encodedData,
    maxFeePerGas: 100000000000,
    maxPriorityFeePerGas: 100000000000
});

const receipt = await tx.wait();
console.log("Fill tx hash:", receipt.hash);
```

### Related

* [Fee Structure](../fee-structure.md) — protocol fees and rate calculation
* [GET /read-partner/api/v1/orders](../api-reference/taker-api.md)
* [GET /read-partner/api/v1/orders/operator-signature](../api-reference/taker-api.md#get-operator-signature)
* [POST /read-ks/api/v1/encode/fill-order-to](../api-reference/taker-api.md#post-read-ks-api-v1-encode-fill-order-to)
