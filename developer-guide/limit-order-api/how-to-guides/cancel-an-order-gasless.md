---
description: >-
  Cancel a limit order off-chain without paying gas by instructing the
  KyberSwap   Operator to stop co-signing the order.
---

# Cancel an Order — Gasless

## Cancel an Order — Gasless

Gasless cancellation works by revoking the Operator's willingness to co-sign a specific order. Because every fill requires a fresh Operator signature, stopping that signature effectively blocks the order from being filled — no on-chain transaction needed.

**Wait time:** Up to 5 minutes if the Operator recently signed the order for an in-flight fill. If the order is far from market price, cancellation is near-instant.

{% hint style="info" %}
For immediate cancellation without any wait, use Hard Cancel and pay a small gas fee.
{% endhint %}

{% hint style="success" %}
**Full demo:** [github.com/KyberNetwork/ks-limit-order-API-demo](https://github.com/KyberNetwork/ks-limit-order-API-demo)
{% endhint %}

### Flow

```
GET /orders  →  POST /cancel-sign  →  sign EIP-712  →  POST /cancel
```

### Step 1 — Get Active Orders

Query your active orders to find the `orderId` to cancel:

```typescript
const { data } = await axios.get(
    "https://limit-order.kyberswap.com/read-ks/api/v1/orders",
    { params: { chainId: 137, maker: signerAddress, status: "active" } }
);

const targetOrderId = data.data[0].id;
```

### Step 2 — Get the Unsigned EIP-712 Cancel Message

Pass one or more `orderIds` to cancel in a single signature:

```typescript
const requestBody = {
    chainId: "137",
    maker: signerAddress,
    orderIds: [targetOrderId]   // can include multiple IDs
};

const { data: cancelData } = await axios.post(
    "https://limit-order.kyberswap.com/write/api/v1/orders/cancel-sign",
    requestBody
);
// cancelData contains: domain, types, message
```

### Step 3 — Sign the Cancel Message

```typescript
const signature = await signer.signTypedData(
    cancelData.domain,
    { CancelOrder: cancelData.types.CancelOrder },
    cancelData.message
);
```

### Step 4 — Submit the Gasless Cancel

```typescript
const signedBody = {
    ...requestBody,
    signature: signature
};

const { data: result } = await axios.post(
    "https://limit-order.kyberswap.com/write/api/v1/orders/cancel",
    signedBody,
    { headers: { Origin: "https://kyberswap.com" } }
);

// result contains: cancelledOrderIds, operatorSignatureExpiry (if recently signed)
console.log("Cancelled:", result.data);
```

The response includes an `operatorSignatureExpiry` timestamp if the Operator had recently signed the order. The order will be fully cancelled once that timestamp passes (max 5 minutes).

### Related

* [Cancel an Order — Hard Cancel](cancel-an-order-hard-cancel.md)
* [POST /write/api/v1/orders/cancel-sign](../api-reference/maker-api.md#post-write-api-v1-orders-cancel-sign)
* [POST /write/api/v1/orders/cancel](../api-reference/maker-api.md#post-write-api-v1-orders-cancel)
