---
description: >-
  Immediately cancel a limit order on-chain by submitting a transaction to the  
  Limit Order contract. Requires a gas fee.
---

# Cancel an Order — Hard Cancel

## Cancel an Order — Hard Cancel

Hard Cancel writes the cancellation directly to the blockchain, making it effective immediately regardless of any in-flight Operator signatures. Use this when you need certainty that an order is cancelled right now.

You can cancel multiple orders in a single transaction to pay gas only once. Alternatively, increment the contract nonce to cancel **all** of your open orders at once.

{% hint style="info" %}
For cancellation without gas, use Gasless Cancel. Expect up to a 5-minute wait.
{% endhint %}

{% hint style="success" %}
**Full demo:** [github.com/KyberNetwork/ks-limit-order-API-demo](https://github.com/KyberNetwork/ks-limit-order-API-demo)
{% endhint %}

### Flow

```
GET /orders  →  POST /encode/cancel-batch-orders  →  send transaction
```

To cancel all orders instead: `POST /encode/increase-nonce → send transaction`

### Step 1 — Get Active Orders

```typescript
const { data } = await axios.get(
    "https://limit-order.kyberswap.com/read-ks/api/v1/orders",
    { params: { chainId: 137, maker: signerAddress, status: "active" } }
);

const targetOrderId = data.data[0].id;
```

### Step 2 — Encode the Cancel Calldata

Pass one or more `orderIds` to cancel in a single transaction:

```typescript
const requestBody = {
    orderIds: [targetOrderId]   // add multiple IDs to batch cancel
};

const { data: encoded } = await axios.post(
    "https://limit-order.kyberswap.com/read-ks/api/v1/encode/cancel-batch-orders",
    requestBody
);
```

#### Alternative: Cancel All Orders

To invalidate all open orders by incrementing the Maker's nonce:

```typescript
const { data: encoded } = await axios.post(
    "https://limit-order.kyberswap.com/read-ks/api/v1/encode/increase-nonce",
    { chainId: 137 }
);
```

### Step 3 — Execute On-chain

```typescript
const tx = await signer.sendTransaction({
    to:    limitOrderContract,
    from:  signerAddress,
    data:  encoded.data.encodedData,
    maxFeePerGas: 100000000000,
    maxPriorityFeePerGas: 100000000000
});

const receipt = await tx.wait();
console.log("Hard cancel tx hash:", receipt.hash);
```

See Contracts & Addresses for the `limitOrderContract` address per chain.

### Related

* [Cancel an Order — Gasless](cancel-an-order-gasless.md)
* [POST /read-ks/api/v1/encode/cancel-batch-orders](../api-reference/maker-api.md#post-read-ks-api-v1-encode-cancel-batch-orders)
* [POST /read-ks/api/v1/encode/increase-nonce](../api-reference/maker-api.md#encode-increase-nonce)
