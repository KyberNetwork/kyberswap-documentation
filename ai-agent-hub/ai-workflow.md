---
description: Connect your AI agent to KyberSwap's APIs and docs
---

# Overview

Connect your AI agent to KyberSwap - a multi-chain decentralized platform connected to 420+ liquidity sources. Swap tokens, create gasless limit orders, zap into concentrated liquidity pools, query token metadata and pool details - across 18 EVM chains, from any MCP-compatible client or any coding agent with shell access. No API keys. No SDK. Public JSON endpoints.

## Overview

KyberSwap provides four ways for AI agents to interact:

**For documentation:**

* [**llms.txt**](read-the-docs-llms.txt-+-mcp.md#llms.txt) - a machine-readable index of the entire KyberSwap documentation. Feed it to any LLM for instant context. No setup, no auth.
* [**Documentation MCP**](read-the-docs-llms.txt-+-mcp.md#documentation-mcp) - a read-only MCP server that lets AI assistants search and retrieve pages from KyberSwap’s documentation in real time. Agents query the docs without leaving their editor. HTTP transport, no auth required.

**For execution:**

* [**Skills**](skills-for-local-agents.md) — markdown procedure files that coding agents read and execute step-by-step using curl, cast, and jq. The only channel that supports real on-chain execution — agents broadcast transactions directly through Foundry.
* [**MCP Server**](mcp-server-for-hosted-agents.md) - 13 tools exposed over the Model Context Protocol. Any MCP-compatible client (Claude Desktop, Claude Code, Cursor, ChatGPT, Windsurf, and others) can discover and call them. The server builds unsigned transactions and EIP-712 typed data but never touches private keys.

[**llms.txt**](read-the-docs-llms.txt-+-mcp.md#llms.txt) and the [**Documentation MCP**](read-the-docs-llms.txt-+-mcp.md#documentation-mcp) help agents understand what KyberSwap can do. [**Skills**](skills-for-local-agents.md) and the [**MCP Server**](mcp-server-for-hosted-agents.md) let agents actually do it.

## Pick the Right Tool

| **Goal**                 | **Local agent (Claude Code, Cursor, Codex)**                                                | **Hosted agent (ChatGPT, Claude.ai, Claude Desktop)**                                                                         |
| ------------------------ | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Read the docs            | [llms.txt](read-the-docs-llms.txt-+-mcp.md#llms.txt) + [Skills](skills-for-local-agents.md) | [llms.txt](read-the-docs-llms.txt-+-mcp.md#llms.txt) + [Documentation MCP](read-the-docs-llms.txt-+-mcp.md#documentation-mcp) |
| Read market data         | [Skills](skills-for-local-agents.md)                                                        | [MCP Server](mcp-server-for-hosted-agents.md)                                                                                 |
| Build swap transactions  | [Skills](skills-for-local-agents.md)                                                        | [MCP Server](mcp-server-for-hosted-agents.md)                                                                                 |
| Execute on-chain         | [Skills](skills-for-local-agents.md) (with Foundry)                                         | Not supported - sign externally                                                                                               |
| Gasless limit orders     | [Skills](skills-for-local-agents.md)                                                        | [MCP Server](mcp-server-for-hosted-agents.md)                                                                                 |
| Zap into liquidity pools | [Skills](skills-for-local-agents.md)                                                        | [MCP Server](mcp-server-for-hosted-agents.md)                                                                                 |

**Local agents** have shell access, can install packages, and can sign and broadcast transactions. The Skills + Foundry combination gives them end-to-end control.

**Hosted agents** cannot install tools or run shell commands. The MCP Server exposes KyberSwap as a set of typed, discoverable tools that any agent can call over stdio - no filesystem required.

{% hint style="info" icon="gear" %}
Switching is free: Both channels hit the same underlying APIs and the same contract addresses. Move from Skills to MCP (or back) without changing anything else in the stack.
{% endhint %}

