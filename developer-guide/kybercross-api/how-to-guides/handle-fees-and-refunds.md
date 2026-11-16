---
description: Fees and refunds on KyberCross API routes
---

# Handle Fees And Refunds

## Overview

KyberCross has three types of fee: `partner_fee`, `protocol_fee` and `additional_fees`.

* `partner_fee` and `protocol_fee` come out of the user's amount. The route's `expected_output_amount` and `min_output_amount` already have them taken out.
* `additional_fees` is paid on top. It does not lower `expected_output_amount`.
* What the bridge provider keeps for itself is already inside its quote output, so it is not listed as a fee.

If a route cannot complete as quoted, funds can be returned through a source leftover, a bridge provider refund or a destination refund. See [Track a refund](handle-fees-and-refunds.md#track-a-refund).

{% hint style="info" %}
These are the fees of the KyberCross API. For fees on the KyberSwap interface, see [Fee Schedule](../../../getting-started/fee-schedule.md).
{% endhint %}

## Fees

### Protocol fee

The protocol fee is the only fee KyberCross charges. It covers the gas to execute the route on the destination chain, so it is charged only on routes that need execution on the destination chain. On routes with a destination swap or gas drop, it is charged on the destination chain, from the bridge output token, before execution.

The amount is set by KyberCross on every quote. It appears in the route plan's `fees` with `type: "protocol_fee"`. It is a fixed amount, not a rate: `rate_ppm` is `0`, and `expected_amount` equals `min_amount`. Check `chain` and `charged_on` for where it is charged.

### Partner fee

You can charge your own partner fee on swaps through your app. KyberCross collects it and sends it to your wallet. Set it on each quote request:

* `partner_fee_bps`: the rate, from `0` through `9999`. `10` is 0.1%. Leave it out, or set `0`, for no fee.
* `partner_fee_recipient`: the wallet that receives the fee. Required when `partner_fee_bps` is greater than `0`.

The partner fee is charged on the source chain, from the bridge input token, before the bridge. It is never charged on the destination chain. It appears in the route plan's `fees` with `type: "partner_fee"` and `charged_on: "bridge_input"`, where `rate_ppm` is `partner_fee_bps * 100`.

For example, with `partner_fee_bps: 10`, a user who sends 1,000 USDC pays a 1 USDC partner fee. The fee is rounded down, so a small amount can result in a zero fee.

### Additional fees

Some bridges charge an extra cost, paid on top in the source transaction as `tx.value`. It does not lower the output, so the user needs this native balance on top of the swap amount.

It is listed in the route plan's `bridge.additional_fees`, not in `fees`. Each entry has `chain`, `token`, `token_decimals` and `amount`.

### Charged fees after execution

The fees actually charged are returned in the execution's `data.fees`, from `GET /api/v1/executions`.

## Refunds

| Refund                 | When                                                                                  | Where the funds go                                                                                                                                                                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Source leftover        | The source swap or bridge does not use all of the tokens                              | Returned automatically, in the same source transaction, to `from_address`                                                                                                                                                                                  |
| Bridge provider refund | The bridge fails, and the bridge provider refunds the transfer                        | Handled by the bridge provider under its own process, generally to the sender on the source chain. Provider-specific deductions may apply. KyberCross tracks the result                                                                                    |
| Destination refund     | The bridge succeeds, but the destination swap cannot be completed before its deadline | KyberCross returns the bridge output token on the destination chain to `to_address`. This may not be the requested destination token. The protocol fee is charged before the refund, and a partner fee already charged on the source chain is not reversed |

{% hint style="info" %}
A refund does not guarantee the original token, the original chain or the full original amount.
{% endhint %}

Track the outcome with `GET /api/v1/executions`. Refund details are returned in `data.refund`.

### Withdraw a failed execution

If an execution is exactly `FAILED` / `UNRECOVERED`, the owner may call `POST /api/v1/executions/{source_tx_hash}/withdrawals/build`, then submit the returned `data.tx` on the destination chain as `data.owner`.

See [**Build owner withdrawal transaction**](../api-reference.md#post-api-v1-executions-source_tx_hash-withdrawals-build) in the API Reference.
