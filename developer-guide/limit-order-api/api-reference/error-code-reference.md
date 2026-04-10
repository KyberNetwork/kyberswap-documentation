---
description: >-
  All HTTP status codes and application-level error codes for the Limit Order
  API.
---

# Error Code Reference

## Error Code Reference

### HTTP Status Codes

| Status | Meaning               | Common cause                                                                         |
| ------ | --------------------- | ------------------------------------------------------------------------------------ |
| `200`  | OK                    | Request succeeded.                                                                   |
| `400`  | Bad Request           | Missing or invalid parameters. Check the `message` field in the response body.       |
| `401`  | Unauthorized          | Invalid or missing authentication. Ensure the `Origin` header is set where required. |
| `404`  | Not Found             | Order ID or resource does not exist.                                                 |
| `429`  | Too Many Requests     | Rate limit exceeded.                                                                 |
| `500`  | Internal Server Error | Unexpected server error. Retry with exponential backoff.                             |

### Application-Level Error Codes

Returned in the response body as `{ "code": ..., "message": "..." }`.

#### Order Creation

| Code   | Message                | Description                                                                             |
| ------ | ---------------------- | --------------------------------------------------------------------------------------- |
| `4001` | Invalid chain ID       | The `chainId` is not supported.                                                         |
| `4002` | Invalid maker asset    | The `makerAsset` address is not a valid ERC-20 on the specified chain.                  |
| `4003` | Invalid taker asset    | The `takerAsset` address is not a valid ERC-20 on the specified chain.                  |
| `4004` | Invalid signature      | The EIP-712 signature does not match the Maker's address.                               |
| `4005` | Order expired          | The `expiredAt` timestamp is in the past.                                               |
| `4006` | Making amount too low  | The `makingAmount` is below the minimum accepted value.                                 |
| `4007` | Insufficient allowance | The Limit Order contract does not have sufficient allowance to cover all active orders. |

#### Order Query

| Code   | Message               | Description                                                                              |
| ------ | --------------------- | ---------------------------------------------------------------------------------------- |
| `4100` | Order not found       | No order exists for the provided ID.                                                     |
| `4101` | Invalid status filter | The `status` parameter is not one of `active`, `open`, `cancelled`, `filled`, `expired`. |

#### Cancellation

| Code   | Message                  | Description                                                      |
| ------ | ------------------------ | ---------------------------------------------------------------- |
| `4200` | Order already cancelled  | The order was already cancelled and cannot be cancelled again.   |
| `4201` | Order already filled     | A filled order cannot be cancelled.                              |
| `4202` | Invalid cancel signature | The EIP-712 cancel signature does not match the Maker's address. |

#### Fill

| Code   | Message                         | Description                                                                                    |
| ------ | ------------------------------- | ---------------------------------------------------------------------------------------------- |
| `4300` | Invalid operator signature      | The Operator signature is invalid or has expired. Fetch a fresh one and retry.                 |
| `4301` | Taking amount exceeds remaining | The requested `takingAmount` exceeds the remaining unfilled amount on the order.               |
| `4302` | Threshold not met               | The fill would result in less `makingAmount` than `thresholdAmount`. Adjust slippage or retry. |

{% hint style="info" %}
If you receive an undocumented error code, include the full request and response body when contacting KyberSwap support.
{% endhint %}
