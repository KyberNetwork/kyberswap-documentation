---
description: >-
  For swaps from supported EIP-2616 tokens, the `permit` parameter allows
  swapping without an approval transaction beforehand.
---

# Permit

## Specification

{% hint style="info" %}
Refer to [evm-swaps.md](evm-swaps.md "mention") for details on where `permit`can be used
{% endhint %}

[EIP-2612](https://eips.ethereum.org/EIPS/eip-2612) tokens can be swapped directly without an initial approval transaction. The client needs to provide an abi-encoded `permit` function calldata (without selector) as a parameter to [#chain-api-v1-route-build](evm-swaps.md#chain-api-v1-route-build "mention") API call. Refer to the [EIP-2612](https://eips.ethereum.org/EIPS/eip-2612) specification for how to sign and encode this call. `permit` function ABI is provided below for reference:

{% code overflow="wrap" %}
```solidity
function permit(address owner, address spender, uint value, uint deadline, uint8 v, bytes32 r, bytes32 s) external
```
{% endcode %}

* `owner`: the swap's token sender
* `spender`: the KyberSwap router address as returned by the GET-route API
* `value`: the amount of token to be swapped
* `deadline`: deadline by which the permit is valid
* `v`, `r`, `s`: a valid `secp256k1` signature from the swap's token sender for the following typed message:

{% code overflow="wrap" %}
```javascript
const domain = {
  name,
  version,
  chainId,
  verifyingContract: await token.getAddress(),
};

const types = {
  Permit: [
    { name: "owner", type: "address" },
    { name: "spender", type: "address" },
    { name: "value", type: "uint256" },
    { name: "nonce", type: "uint256" },
    { name: "deadline", type: "uint256" },
  ],
};

const message = {
  owner,
  spender,
  value,
  nonce,
  deadline,
};
```
{% endcode %}

## Example

```mjs
import { ethers } from "ethers";
import fetch from "node-fetch";

const rpcUrl = "https://ethereum.publicnode.com";
const provider = new ethers.JsonRpcProvider(rpcUrl);
const signer = new ethers.Wallet(process.env.PRIV_KEY, provider);

const clientId = "permit-test";

const erc20Abi = [
  "function name() view returns (string)",
  "function nonces(address) view returns (uint256)",
  "function version() view returns (string)",
];

async function signPermit(signer, token, spender, value, chainId) {
  const owner = await signer.getAddress();
  const nonce = await token.nonces(owner);
  const name = await token.name();
  let version = "1";
  try {
    version = await token.version();
  } catch {}

  const deadline = Math.floor(Date.now() / 1000) + 3600;

  const domain = {
    name,
    version,
    chainId,
    verifyingContract: await token.getAddress(),
  };

  const types = {
    Permit: [
      { name: "owner", type: "address" },
      { name: "spender", type: "address" },
      { name: "value", type: "uint256" },
      { name: "nonce", type: "uint256" },
      { name: "deadline", type: "uint256" },
    ],
  };

  const message = {
    owner,
    spender,
    value,
    nonce,
    deadline,
  };

  const sig = await signer.signTypedData(domain, types, message);
  const { v, r, s } = ethers.Signature.from(sig);

  return { v, r, s, deadline };
}

async function getRoute(tokenIn, tokenOut, amountIn) {
  const url =
    `https://aggregator-api.kyberswap.com/ethereum/api/v1/routes` +
    `?tokenIn=${tokenIn}&tokenOut=${tokenOut}&amountIn=${amountIn}`;

  const res = await fetch(url, {
    headers: { "X-Client-Id": clientId },
  });

  const j = await res.json();
  if (!j.data) {
    throw new Error("no route: " + JSON.stringify(j));
  }
  const routeSummary = j.data.routeSummary;
  console.log(
    `Got a route to swap from ${routeSummary.amountIn} ${
      routeSummary.tokenIn
    } to ${routeSummary.amountOut} ${routeSummary.tokenOut}`,
  );
  return j.data;
}

async function buildRoute(route, permit, sender, amountIn) {
  const body = {
    routeSummary: route.routeSummary,
    sender,
    recipient: sender,
    slippageTolerance: 10,
    permit: ethers.AbiCoder.defaultAbiCoder().encode(
      [
        "address",
        "address",
        "uint256",
        "uint256",
        "uint8",
        "bytes32",
        "bytes32",
      ],
      [
        sender,
        route.routerAddress,
        amountIn,
        permit.deadline,
        permit.v,
        permit.r,
        permit.s,
      ],
    ),
    deadline: permit.deadline + 300,
    enableGasEstimation: false,
  };

  const res = await fetch(
    "https://aggregator-api.kyberswap.com/ethereum/api/v1/route/build",
    {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "X-Client-Id": clientId,
      },
      body: JSON.stringify(body),
    },
  );

  const j = await res.json();
  if (!j.data) {
    throw new Error("build failed: " + JSON.stringify(j));
  }
  return j.data;
}

async function executeSwap(routerAddress, calldata, signer) {
  const tx = await signer.sendTransaction({
    to: routerAddress,
    data: calldata,
  });
  return tx.wait();
}

async function main() {
  const signerAddr = await signer.getAddress();

  const tokenIn = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48"; // USDC
  const tokenOut = "0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE"; // ETH pseudo-address
  const amountIn = 100000000n; // USDC 100 * 1e6

  const route = await getRoute(tokenIn, tokenOut, amountIn);
  const router = route.routerAddress;

  const token = new ethers.Contract(tokenIn, erc20Abi, provider);
  const net = await provider.getNetwork();

  const permit = await signPermit(signer, token, router, amountIn, net.chainId);

  const built = await buildRoute(route, permit, signerAddr, amountIn);

  const receipt = await executeSwap(router, built.data, signer);
  console.log(receipt);
}

main().catch(console.error);

```
