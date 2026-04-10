---
description: >-
  Sign and submit a gasless limit order as a Maker using the KyberSwap Limit  
  Order API.
---

# Place a Limit Order

## Place a Limit Order

Makers create limit orders by signing an EIP-712 message off-chain — no gas required. The signed order is stored in KyberSwap's off-chain orderbook and settled on-chain when a Taker fills it.

{% hint style="success" %}
**Full demo:** [github.com/KyberNetwork/ks-limit-order-API-demo](https://github.com/KyberNetwork/ks-limit-order-API-demo)
{% endhint %}

### Flow

```
POST /sign-message  →  sign EIP-712  →  check allowance  →  POST /orders
```

### Step 1 — Get the Unsigned EIP-712 Message

Call `POST /write/api/v1/orders/sign-message` with the order parameters:

```typescript
const requestBody = {
    chainId: "137",                      // Polygon
    makerAsset: "0x2791bca1...",         // USDC
    takerAsset: "0x1C954E8f...",         // KNC
    maker: signerAddress,
    allowedSenders: [signerAddress],     // optional: restrict who can fill
    makingAmount: "10000",               // 0.01 USDC (6 decimals)
    takingAmount: "20000000000000000",   // 0.02 KNC (18 decimals)
    expiredAt: Math.floor(Date.now() / 1000) + 3600  // expires in 1 hour
};

const { data } = await axios.post(
    "https://limit-order.kyberswap.com/write/api/v1/orders/sign-message",
    requestBody
);
// data contains: domain, types, message (unsigned EIP-712)
```

{% hint style="info" %}
`makingAmount` and `takingAmount` are raw token amounts in the smallest unit (wei). Use the token contract's `decimals()` to convert.
{% endhint %}

### Step 2 — Check and Set Allowance

The Limit Order contract must be approved to spend the Maker's `makerAsset`. Check the current active making amount first — allowance must cover all open orders, not just the new one:

```typescript
// Get total active making amount for this token
const { data: activeAmount } = await axios.get(
    "https://limit-order.kyberswap.com/read-ks/api/v1/orders/active-making-amount",
    { params: { chainId: 137, makerAsset: makerAsset, maker: signerAddress } }
);

const totalNeeded = BigInt(activeAmount.data) + BigInt(requestBody.makingAmount);

// Check current allowance against LO contract
const allowance = await tokenContract.allowance(signerAddress, limitOrderContract);

if (allowance < totalNeeded) {
    const tx = await tokenContract.approve(limitOrderContract, totalNeeded);
    await tx.wait();
}
```

See Contracts & Addresses for the `limitOrderContract` address per chain.

### Step 3 — Sign the EIP-712 Message

```typescript
const signature = await signer.signTypedData(
    data.domain,
    { Order: data.types.Order },   // use the primaryType returned by the API
    data.message
);
```

### Step 4 — Submit the Order

Append `salt` and `signature` to the original request body and POST to `/write/api/v1/orders`:

```typescript
const signedBody = {
    ...requestBody,
    salt: data.message.salt,
    signature: signature
};

const { data: order } = await axios.post(
    "https://limit-order.kyberswap.com/write/api/v1/orders",
    signedBody
);

console.log("Order created:", order.data.orderId);
```

The response includes an `orderId` which can be used to track, query, or cancel the order.

### Related

* [Cancel an Order — Gasless](cancel-an-order-gasless.md)
* [Cancel an Order — Hard Cancel](cancel-an-order-hard-cancel.md)
* [POST /write/api/v1/orders/sign-message](../api-reference/maker-api.md)
* [POST /write/api/v1/orders](../api-reference/maker-api.md)
