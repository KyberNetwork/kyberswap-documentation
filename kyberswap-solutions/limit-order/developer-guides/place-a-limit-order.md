---
description: Make Limit Orders On The Market
---

# Place A Limit Order

## Signing data

* `Limit Order` mechanism requires makers to sign their order before it can be processed by our smart contract.
* To place an order off chain, makers have to provide a signature of the order follow [Sign Typed Data v4](https://docs.metamask.io/guide/signing-data.html#sign-typed-data-v4). If makers use our UI, that process is very straightforward. In case makers don't use out UI, but directly uses our API to place an order, we have an API to support makers sign their order easily.
* After signing, signature of the order will be used to fill order on chain by call `fillOrderTo()` or `fillBatchOrdersTo()` method of our smart contract
