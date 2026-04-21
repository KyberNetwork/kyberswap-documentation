---
description: >-
  Pre-built agent skills for trading and managing liquidity via KyberSwap APIs
  from local AI coding agents
---

# Skills - For Local Agents

Structured context files that give AI coding agents the ability to trade, manage liquidity, and query DeFi data across 18 EVM chains via KyberSwap APIs.

Skills are markdown files that AI agents read and follow as procedural instructions. No SDK, no library — the agent reads the skill, understands the workflow, and executes it using standard tools (`curl`, `cast`, `jq`).

**Repository:**  [github.com/KyberNetwork/kyberswap-skills](https://github.com/KyberNetwork/kyberswap-skills)

## Install

```bash
/install-plugin <https://github.com/kyberswap/kyberswap-skills>
```

Or load locally for development:

```bash
claude --plugin-dir /path/to/kyberswap-skills
```

No API keys required. KyberSwap APIs are public.

## How Skills Work

The execution flow is always the same:

```
User Request → Agent reads SKILL.md → API calls (curl) → User confirmation → On-chain execution (cast)
```

1. The agent receives a user request (e.g., “swap 1 ETH to USDC on Base”).
2. The agent reads the relevant `SKILL.md` file.
3. The skill contains step-by-step instructions: resolve tokens, call the API, format the response, ask for confirmation.
4. The agent follows the instructions using standard tools — `curl` for API calls, `cast` for on-chain execution.
5. State-changing actions always require explicit user confirmation (unless using a `fast` variant).

## Available Skills

### Price Discovery & Market Data

| Skill        | Description                                                                                                                             |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `quote`      | Get the best swap route and expected output for a token pair. Includes gas estimates, route path, and safety checks.                    |
| `token-info` | Look up token metadata, live USD price, decimals, and security assessment (honeypot/fee-on-transfer detection). Supports batch queries. |
| `pool-info`  | Query liquidity pool details — TVL, 24h volume, fee tier, APR, LP APR, and token pair info across all indexed DEXes.                    |

### Swap Lifecycle

| Skill           | Description                                                                                                                         |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `swap-build`    | Build a swap transaction with encoded calldata. Applies intelligent slippage defaults. Requires user confirmation.                  |
| `swap-simulate` | Dry-run a swap transaction using `cast call` — no gas spent, no state changed. Validates the route before execution.                |
| `swap-execute`  | Broadcast a built swap transaction on-chain via Foundry’s `cast send`. Supports keystore, env var, Ledger, and Trezor wallets.      |
| `swap-status`   | Check whether a submitted transaction succeeded or failed. Decodes revert reasons for failed transactions.                          |
| `swap-approve`  | Manage ERC-20 token approvals for the KyberSwap router. Check, set, or revoke allowances. Handles the USDT zero-first special case. |

### Swap Fast Path

| Skill               | Description                                                                                                             |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `swap-execute-fast` | Build and execute a swap in one step with no confirmation prompts. Uses shell scripts. **For trusted automation only.** |

### Gasless Limit Orders

| Skill           | Description                                                                                                                                                       |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `limit-order`   | Create, query, and cancel gasless limit orders. Orders are signed off-chain via EIP-712 and settled on-chain when filled. Supports gasless and hard cancellation. |
| `order-manager` | View and analyze limit orders across all statuses — open, partially filled, filled, cancelled, expired. Shows fill progress and portfolio summary.                |

### Limit Order Fast Path

| Skill              | Description                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------------ |
| `limit-order-fast` | Sign and create a limit order in one step with no confirmation. **For trusted automation only.** |

### Concentrated Liquidity

| Skill              | Description                                                                                                                                                            |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `zap`              | Zap into or out of concentrated liquidity positions in one transaction. Handles token ratio calculation, swaps, and deposits automatically. Supports 71 DEX protocols. |
| `position-manager` | View and analyze DeFi liquidity positions across chains — in-range/out-of-range status, APR, unclaimed fees, and actionable suggestions.                               |

### Zap Fast Path

| Skill      | Description                                                                                |
| ---------- | ------------------------------------------------------------------------------------------ |
| `zap-fast` | Build and execute a zap in one step with no confirmation. **For trusted automation only.** |

### Diagnostics

| Skill            | Description                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `error-handling` | Comprehensive error diagnosis and resolution guide covering API errors, pre-transaction failures, and on-chain reverts. |

## Safety Model

Skills follow a **safe by default** pattern:

* **Safe path** (`quote`, `swap-build`, `swap-execute`, `limit-order`, `zap`): Every state-changing action requires explicit user confirmation. The agent presents transaction details and waits for approval.
* **Fast path** (`swap-execute-fast`, `limit-order-fast`, `zap-fast`): Skip all confirmations. Marked `EXTREMELY DANGEROUS`. Designed for trusted automation pipelines where the operator controls the parameters.
* **Read-only** (`token-info`, `pool-info`, `position-manager`, `order-manager`, `swap-simulate`, `swap-status`): Never modify blockchain state.

Built-in safety checks on all paths:

* Honeypot detection
* Fee-on-transfer (FOT) warnings
* Address validation (rejects zero address and native sentinel for ERC-20 operations)
* Router address verification
* Dust/uneconomical trade warnings (sub-$0.10)
* Price impact evaluation

## Supported Exchanges and Networks

Refer to [Supported Exchanges and Networks](skills-for-local-agents.md#supported-exchanges-and-networks).

## Architecture

Skills connect to three KyberSwap API services:

| Service        | Base URL                       | Purpose                                     |
| -------------- | ------------------------------ | ------------------------------------------- |
| Aggregator API | `aggregator-api.kyberswap.com` | Swap routing and calldata building          |
| Token API      | `token-api.kyberswap.com`      | Token metadata, pricing, honeypot detection |
| Earn Service   | `earn-service.kyberswap.com`   | Pool information and position management    |

All API requests include the `X-Client-Id: ai-agent-skills` header.

On-chain execution uses [Foundry’s `cast`](https://book.getfoundry.sh/reference/cast/) for transaction broadcasting, simulation, and receipt retrieval.

### Key Contracts

* [KyberSwap Aggregator Router](../developer-guide/aggregator-api/contracts.md)
* [DSLOProtocol (Limit Orders)](../developer-guide/limit-order-api/contracts-and-addresses.md)
* [KSZapRouterPosition (Zap)](../developer-guide/zap-as-a-service-zaas-api/contracts-and-addresses.md)

### Token Resolution

For tokens not in the built-in registry, the resolution chain is:

1. KyberSwap Token API — whitelisted tokens
2. CoinGecko API — search by symbol, verify decimals
3. Manual user input

## Prerequisites

| Dependency       | Required for                                                         |
| ---------------- | -------------------------------------------------------------------- |
| Foundry (`cast`) | `swap-execute`, `swap-simulate`, `swap-status`, all `-fast` variants |
| `curl`, `jq`     | All `-fast` script-based skills                                      |
| `bc`             | `limit-order-fast`                                                   |
| Wallet           | On-chain execution — keystore, `$PRIVATE_KEY`, Ledger, or Trezor     |

## Workflows

**Get a quote:**

```
User: "How much USDC would I get for 1 ETH on Arbitrum?"
→ Agent invokes: quote
```

**Swap tokens:**

```
User: "Swap 1 ETH to USDC on Base"
→ Agent invokes: swap-build → user confirms → swap-execute → swap-status
```

**Create a limit order:**

```
User: "Buy 1 ETH at $2,000 with USDC on Ethereum"
→ Agent invokes: limit-order → user confirms → order signed and submitted
```

**Add liquidity:**

```
User: "Zap 1000 USDC into the best ETH/USDC pool on Arbitrum"
→ Agent invokes: pool-info → user selects pool → zap → user confirms → executed
```
