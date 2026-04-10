---
description: Off-Chain Relay, On-Chain Settlement
---

# Limit Order API

## Overview & Capabilities

KyberSwap Limit Order lets users trade at a predefined rate that is automatically settled on-chain when the market reaches their target price. Orders are created gaslessly off-chain, stored in a KyberSwap orderbook, and filled by a network of Takers who execute the trade on-chain.

**Base URL:** `https://limit-order.kyberswap.com`

***

### Roles

| Role      | Description                                                                                               |
| --------- | --------------------------------------------------------------------------------------------------------- |
| **Maker** | Creates a limit order by signing an EIP-712 message off-chain. No gas required to place.                  |
| **Taker** | Discovers open orders and fills them on-chain, earning the spread as profit. Pays gas and a protocol fee. |

### How It Works

1. **Maker** calls `/write/api/v1/orders/sign-message` → signs the returned EIP-712 message → posts the signed order to `/write/api/v1/orders`.
2. The order is stored off-chain in KyberSwap's orderbook.
3. **Taker** queries open orders, requests an Operator signature, encodes the fill calldata, and executes on-chain.
4. The Limit Order contract settles the trade, transferring assets between Maker and Taker atomically.

### What the API Can Do

* Place limit orders gaslessly (Maker signs off-chain, no gas)
* Fill single or batched limit orders on-chain (Taker)
* Cancel orders gaslessly (up to 5-minute wait) or immediately on-chain (Hard Cancel with gas)
* Query open orders sorted by best rate
* Query a Maker's active making amount per token (for allowance management)
* Query supported token pairs and contract addresses

### What the API Cannot Do

* Guarantee fill time — orders are filled only when a Taker finds them profitable
* Provide an order book UI — the API returns raw order data; visualization is the integrator's responsibility
* Fill orders without an Operator signature — every fill requires a fresh KyberSwap Operator co-signature

***

### Endpoint Index

#### General

| Method | Path                                       | Description                              |
| ------ | ------------------------------------------ | ---------------------------------------- |
| `GET`  | `/read-partner/api/v1/orders/pairs`        | List all supported trading pairs         |
| `GET`  | `/read-ks/api/v1/configs/contract-address` | Get deployed contract addresses by chain |

#### Maker

| Method | Path                                          | Description                                         |
| ------ | --------------------------------------------- | --------------------------------------------------- |
| `POST` | `/write/api/v1/orders/sign-message`           | Get the unsigned EIP-712 create order message       |
| `POST` | `/write/api/v1/orders`                        | Submit a signed order to the orderbook              |
| `GET`  | `/read-ks/api/v1/orders`                      | Get all orders for a Maker address                  |
| `GET`  | `/read-ks/api/v1/orders/active-making-amount` | Get the aggregated active making amount per token   |
| `POST` | `/write/api/v1/orders/cancel-sign`            | Get the unsigned EIP-712 gasless cancel message     |
| `POST` | `/write/api/v1/orders/cancel`                 | Submit a signed gasless cancel request              |
| `POST` | `/read-ks/api/v1/encode/cancel-batch-orders`  | Encode on-chain batch cancel calldata               |
| `POST` | `/read-ks/api/v1/encode/increase-nonce`       | Encode on-chain nonce increase to cancel all orders |

#### Taker

| Method | Path                                             | Description                                        |
| ------ | ------------------------------------------------ | -------------------------------------------------- |
| `GET`  | `/read-partner/api/v1/orders`                    | Get open orders sorted by best rate                |
| `GET`  | `/read-partner/api/v1/orders/operator-signature` | Get the KyberSwap Operator co-signature for a fill |
| `POST` | `/read-ks/api/v1/encode/fill-order-to`           | Encode calldata to fill a single order             |
| `POST` | `/read-ks/api/v1/encode/fill-batch-orders-to`    | Encode calldata to fill multiple orders in one tx  |

For fee categories and the rate calculation formula, see Fee Structure. For error codes, see [Error Code Reference.](api-reference/error-code-reference.md)
