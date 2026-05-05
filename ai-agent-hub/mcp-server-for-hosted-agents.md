---
description: >-
  Trade, manage liquidity, and build transactions via Model Context Protocol
  from any hosted AI agent
---

# MCP Server - For Hosted Agents

13 tools over the Model Context Protocol. Read-only and calldata-building only — the server never holds private keys, never signs, never broadcasts. It returns unsigned transaction objects and EIP-712 typed data for the user to sign with their own wallet.

**Repository:**  [github.com/KyberNetwork/kyberswap-mcp](https://github.com/KyberNetwork/kyberswap-mcp)

## What is MCP?

The [Model Context Protocol](https://modelcontextprotocol.io/) is an open standard that lets AI applications connect to external tools and data sources. The KyberSwap MCP Server gives any MCP-compatible AI client access to:

* Swap quotes and transaction building across 18 EVM chains
* Token metadata, pricing, and security assessment
* Gasless limit order creation and management
* Concentrated liquidity pool discovery and zap operations
* Transaction simulation and status checking

## Setup

{% tabs %}
{% tab title="Claude Code" %}
Add the server to your project or user scope:

```json
// .mcp.json
{
  "mcpServers": {
    "kyberswap": {
      "command": "node",
      "args": ["/path/to/kyberswap-mcp/dist/index.js"]
    }
  }
}
```


{% endtab %}

{% tab title="Claude Desktop" %}
```json
// claude_desktop_config.json
{
  "mcpServers": {
    "kyberswap": {
      "command": "node",
      "args": ["/path/to/kyberswap-mcp/dist/index.js"]
    }
  }
}
```


{% endtab %}

{% tab title="Cursor" %}
```json
// .cursor/mcp.json
{
  "mcpServers": {
    "kyberswap": {
      "command": "node",
      "args": ["/path/to/kyberswap-mcp/dist/index.js"]
    }
  }
}
```


{% endtab %}
{% endtabs %}

### Other MCP-Compatible Tools

Any client that supports the MCP specification can connect via stdio transport. Point it to the compiled server entry point at `dist/index.js`.

### Build from Source

```bash
git clone <https://github.com/KyberNetwork/kyberswap-mcp.git>
cd kyberswap-mcp
npm install
npm run build
```

No API keys required. KyberSwap APIs are public.

## Available Tools

### Price Discovery & Market Data

| Tool            | Description                                                                                                                                                     |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `get-quote`     | Get the best swap route from the KyberSwap Aggregator. Returns exchange rate, route details, gas estimate, USD values, price impact, and token safety warnings. |
| `token-info`    | Retrieve token metadata, live USD price, and security assessment. Accepts single tokens or comma-separated lists (e.g., `"USDC, WBTC, ETH"`).                   |
| `get-pool-info` | Query liquidity pools — TVL, 24h volume, APR, LP APR, earned fees. Filter by token pair, DEX protocol, or sort by metrics.                                      |

### Swap Transaction Building

| Tool            | Description                                                                                                                                                                  |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `swap-build`    | Construct an unsigned swap transaction. Returns the complete transaction object (`to`, `data`, `value`) ready for external wallet signing. Routes expire after \~30 seconds. |
| `swap-simulate` | Dry-run a swap transaction via `eth_call` — no gas or funds required. Validates route validity before signing. Decodes revert reasons on failure.                            |
| `swap-status`   | Check on-chain status of a submitted transaction. Returns receipt data, gas used, and explorer URL. Replays failed transactions to decode revert reasons.                    |

### Gasless Limit Orders

| Tool                        | Description                                                                                                                                                                   |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `limit-order-build`         | Construct a gasless limit order. Returns EIP-712 typed data for wallet signing. Validates maker asset, checks price deviation from market, and returns approval requirements. |
| `limit-order-submit`        | Submit a signed limit order to KyberSwap. Called after the user signs the EIP-712 data from `limit-order-build`. Returns the order ID.                                        |
| `limit-order-cancel-build`  | Build a gasless cancellation for one or more limit orders. Returns EIP-712 typed data to sign. Gasless window is \~90 seconds from order creation.                            |
| `limit-order-cancel-submit` | Submit the signed gasless cancellation.                                                                                                                                       |

### Portfolio & Position Management

| Tool               | Description                                                                                                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `order-manager`    | Query limit orders for a wallet. Filter by status (open, partially filled, filled, cancelled, expired). Shows fill progress, target vs effective prices, and remaining amounts. |
| `position-manager` | Monitor liquidity positions across chains. Returns total value, unclaimed fees, 30-day APR, price ranges, and protocol details. Filter by chain, protocol, or status.           |

### Concentrated Liquidity

| Tool  | Description                                                                                                                                                                    |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `zap` | Build concentrated liquidity transactions — zap-in (add liquidity) or zap-out (remove liquidity). Supports tick/price bounds, full range, partial withdrawal, and NFT burning. |

## Workflows

### Swap

```
get-quote → swap-build → swap-simulate → sign externally → broadcast → swap-status
```

### Limit Order

```
limit-order-build → ensure token approval → sign EIP-712 → limit-order-submit → order-manager (monitor)
```

### Add Liquidity

```
get-pool-info → user confirms pool → zap (in) → swap-simulate → sign externally → broadcast
```

### Cancel Order

```
order-manager (get order IDs) → limit-order-cancel-build → sign EIP-712 → limit-order-cancel-submit
```

## Safety Features

The MCP server includes built-in safety checks on every operation:

* **Honeypot detection** — flags tokens with transfer restrictions
* **Fee-on-transfer (FOT) detection** — adjusts expected amounts for taxed tokens
* **Price deviation checks** — blocks limit orders >50% below market, warns at >10%
* **Price impact evaluation** — warns at >1% impact, blocks at >15%
* **Balance sufficiency checks** — verifies the sender has enough tokens
* **Route expiration warnings** — routes are valid for \~30 seconds
* **Gasless cancel window tracking** — warns when the 90-second free cancellation window expires

## Supported Exchanges and Networks

Refer to [Supported Exchanges and Networks](mcp-server-for-hosted-agents.md#supported-exchanges-and-networks).

Each chain has a default public RPC URL that can be overridden via environment variables (e.g., `RPC_URL_ETHEREUM`, `RPC_URL_ARBITRUM`).

## Architecture

### Transport

Stdio (stdin/stdout JSON-RPC) via `@modelcontextprotocol/sdk`. This is the standard MCP transport for local integrations.

### API Services

| Service      | Base URL                       | Purpose                                     |
| ------------ | ------------------------------ | ------------------------------------------- |
| Aggregator   | `aggregator-api.kyberswap.com` | Swap routing and calldata building          |
| Token API    | `token-api.kyberswap.com`      | Token metadata, pricing, honeypot detection |
| Limit Order  | `limit-order.kyberswap.com`    | Gasless limit order lifecycle               |
| Earn Service | `earn-service.kyberswap.com`   | Pool info, position management              |
| Zap API      | `zap-api.kyberswap.com`        | Concentrated liquidity operations           |

All API requests include the `X-Client-Id: ai-agent-mcp` header and have a 15-second timeout.

### On-Chain Reads

The server uses [viem](https://viem.sh/) public clients for `eth_call` (simulation) and `getTransactionReceipt` (status checks) via the configured RPC URLs.

### Key Contracts

* [KyberSwap Aggregator Router](../developer-guide/aggregator-api/contracts.md)
* [DSLOProtocol (Limit Orders)](../developer-guide/limit-order-api/contracts-and-addresses.md)
* [KSZapRouterPosition (Zap)](../developer-guide/zap-as-a-service-zaas-api/contracts-and-addresses.md)

### Key Design Principle

The MCP server **never holds private keys**. It constructs unsigned calldata or EIP-712 typed data and returns it to the client. The user signs with their own wallet infrastructure — hardware wallet, browser extension, or external signer.

## Configuration

### Environment Variables

All optional. Override default RPC endpoints per chain:

| Variable           | Default                |
| ------------------ | ---------------------- |
| `RPC_URL_ETHEREUM` | LlamaRPC               |
| `RPC_URL_BSC`      | Binance public RPC     |
| `RPC_URL_ARBITRUM` | Arbitrum public RPC    |
| `RPC_URL_{CHAIN}`  | Chain-specific default |

No wallet secrets, API keys, or other sensitive configurations are required.

### Dependencies

* Node.js 18+
* `@modelcontextprotocol/sdk` ^1.12.0
* `viem` ^2.23.0
* `zod` ^3.24.0

## Resources

* **Repository:** [github.com/KyberNetwork/kyberswap-mcp](https://github.com/KyberNetwork/kyberswap-mcp)
* **KyberSwap Skills (for local agents):** [github.com/KyberNetwork/kyberswap-skills](https://github.com/KyberNetwork/kyberswap-skills)
* **MCP Specification:** [modelcontextprotocol.io](https://modelcontextprotocol.io/)
