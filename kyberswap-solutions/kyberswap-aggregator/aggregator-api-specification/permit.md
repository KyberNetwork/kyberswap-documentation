---
description: >-
  For swaps from supported EIP-2616 tokens, the `permit` parameter allows
  swapping without an approval transaction beforehand.
---

# Permit

{% hint style="info" %}
Refer to [evm-swaps.md](evm-swaps.md "mention") for details on where `permit`can be used
{% endhint %}

[EIP-2612](https://eips.ethereum.org/EIPS/eip-2612) tokens can be swapped directly without an initial approval transaction. The client needs to provide a directly usable `permit` calldata as a parameter to [#chain-api-v1-route-build](evm-swaps.md#chain-api-v1-route-build "mention") API call. Refer to the [EIP-2612](https://eips.ethereum.org/EIPS/eip-2612) specification for how to sign and encode this call. `permit` ABI is provided below for reference:

{% code overflow="wrap" %}
```solidity
function permit(address owner, address spender, uint value, uint deadline, uint8 v, bytes32 r, bytes32 s) external
```
{% endcode %}

* `owner`: the swap's token sender
* `spender`: the KyberSwap router address as returned by the GET-route API
* `value`: the amount of token to be swapped
* `deadline`: deadline by which the permit is valid
* `v`, `r`, `s`: a valid `secp256k1` signature from the swap's token sender for the following message:

{% code overflow="wrap" %}
```solidity
keccak256(abi.encodePacked(
   hex"1901",
   DOMAIN_SEPARATOR,
   keccak256(abi.encode(
            keccak256("Permit(address owner,address spender,uint256 value,uint256 nonce,uint256 deadline)"),
            owner,
            spender,
            value,
            nonce,
            deadline))
))
```
{% endcode %}
