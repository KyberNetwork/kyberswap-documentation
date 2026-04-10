---
description: >-
  Use EIP-2612 (ERC-20) or EIP-4494 (NFT) permit signatures with the  
  KSZapRouterPositionPermit contract to approve and zap in a single transaction.
---

# Using Permit to Skip separate approval step

## Using Permit to Skip Separate Approval Step

By default, a zap requires the user to send a separate approval transaction before the zap itself. Permit lets you skip that step by attaching an off-chain signature to the `BuildRoute` request — the router verifies and applies the approval atomically as part of the zap.

Permit is supported for two asset types:

| Asset              | Standard | When to use                                                                       |
| ------------------ | -------- | --------------------------------------------------------------------------------- |
| ERC-20 input token | EIP-2612 | Zap In with a fungible token that supports `permit()`                             |
| Position NFT       | EIP-4494 | Zap Out or Zap Migrate where the router needs to transfer the user's position NFT |

### Prerequisites

* Use the `KSZapRouterPositionPermit` contract address for the target chain. See Contracts & Addresses.
* The ERC-20 token must implement `permit(owner, spender, value, deadline, v, r, s)` (EIP-2612).
* The NFT contract must implement `permit(spender, tokenId, deadline, sig)` (EIP-4494).

### How It Works

1. Sign a permit message off-chain with the user's wallet (no gas).
2. Pass the permit signature(s) in the `BuildRoute` request body, keyed by token address or NFT token ID.
3. The router applies the permit and executes the zap in one transaction.

### Permit Payload Format

The `permit` field in any `BuildRoute` request body is a map from **token address** (for ERC-20) or **NFT token ID** (for position NFTs) to the hex-encoded permit signature:

```json
{
  "sender": "0xUserAddress",
  "recipient": "0xUserAddress",
  "route": "<encoded route from GetRoute>",
  "deadline": 1800000000,
  "permit": {
    "<token_address_or_nft_id>": "<permit_signature>"
  }
}
```

You can include multiple permits in one request if the operation requires approvals for more than one asset:

```json
{
  "permit": {
    "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48": "0xabc...def",
    "12345": "0x123...456"
  }
}
```

### Step 1 — Sign the Permit

#### ERC-20 (EIP-2612)

```javascript
const domain = {
  name: await tokenContract.name(),
  version: '1',
  chainId: chainId,
  verifyingContract: tokenAddress,
};

const types = {
  Permit: [
    { name: 'owner',    type: 'address' },
    { name: 'spender',  type: 'address' },
    { name: 'value',    type: 'uint256' },
    { name: 'nonce',    type: 'uint256' },
    { name: 'deadline', type: 'uint256' },
  ],
};

const deadline = Math.floor(Date.now() / 1000) + 1800; // 30 min

const message = {
  owner:   userAddress,
  spender: routerAddress,   // KSZapRouterPositionPermit address
  value:   amountIn,
  nonce:   await tokenContract.nonces(userAddress),
  deadline,
};

const signature = await signer.signTypedData(domain, types, message);
```

#### Position NFT (EIP-4494)

```javascript
const domain = {
  name: await nftContract.name(),
  version: '1',
  chainId: chainId,
  verifyingContract: nftContractAddress,
};

const types = {
  Permit: [
    { name: 'spender',  type: 'address' },
    { name: 'tokenId',  type: 'uint256' },
    { name: 'nonce',    type: 'uint256' },
    { name: 'deadline', type: 'uint256' },
  ],
};

const deadline = Math.floor(Date.now() / 1000) + 1800;

const message = {
  spender:  routerAddress,   // KSZapRouterPositionPermit address
  tokenId:  positionId,
  nonce:    await nftContract.nonces(positionId),
  deadline,
};

const signature = await signer.signTypedData(domain, types, message);
```

{% hint style="info" %}
The exact EIP-4494 domain and nonce method may vary by NFT contract. Check the position manager contract for the specific DEX you are using.
{% endhint %}

### Step 2 — Build the Route with the Permit

Pass the signature(s) in the `permit` map, keyed by the token address (ERC-20) or the token ID as a string (NFT):

**ERC-20 example (Zap In):**

```json
{
  "sender": "0xUserAddress",
  "recipient": "0xUserAddress",
  "route": "<route from GetInRoute>",
  "deadline": 1800000000,
  "permit": {
    "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48": "0xabc...def"
  }
}
```

**NFT example (Zap Out or Zap Migrate):**

```json
{
  "sender": "0xUserAddress",
  "recipient": "0xUserAddress",
  "route": "<route from GetOutRoute or GetMigrateRoute>",
  "deadline": 1800000000,
  "permit": {
    "12345": "0x123...456"
  }
}
```

### Step 3 — Send the Transaction

Use `calldata`, `value`, and `routerAddress` from the `BuildRoute` response to submit:

```javascript
const tx = await signer.sendTransaction({
  to:    buildResponse.routerAddress,
  data:  buildResponse.calldata,
  value: buildResponse.value,
  gasLimit: routeResponse.gas * 2,
});
```

{% hint style="warning" %}
If the token or NFT contract does not implement the expected permit standard correctly, the transaction will revert. Verify permit support before using this flow.
{% endhint %}
