---
description: Take Limit Orders From The Market
---

# Fill A Limit Order

## Limit order execution

1. KyberSwap users can place a Limit Order through the interface at [KyberSwap](https://kyberswap.com/limit/) with no gas fee
2. Anyone can fetch these off-chain signed orders using Limit Order API to perform trade by filling the order on-chain
3. To fill the order, the taker can call the `fillOrder`, `fillOrderTo`, `fillBatchOrderTo` or `fillOrderToWithPermit` function on the Smart Contract.

{% hint style="info" %}
Note

* Trades buyer and seller should approve their tokens to be used by KyberSwap limit order contract
* Please refer to [Limit Order Contract Addresses](../contracts/limit-order-contract-addresses.md) for the latest contract addresses
{% endhint %}

The encoding API can be used to make it easier. In the case of `fillBatchOrderTo`, KyberSwap's encoding API even returns encodeData so that better orders will be filled first.
