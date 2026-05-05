---
description: Search and query KyberSwap docs via llms.txt and Documentation MCP
---

# Read the Docs (llms.txt + MCP)

Two surfaces help agents discover and understand KyberSwap before taking action: a flat documentation index that works everywhere, and the MCP Server's typed tool manifest for agents that prefer structured, schema-driven discovery.

## llms.txt

A structured, LLM-optimised index of every KyberSwap developer doc, API endpoint, and integration guide, following the llmstxt.org standard. Works with any AI tool - paste the URL into a chat, attach it to a system prompt, or pipe it into a RAG pipeline.

### URL

[https://docs.kyberswap.com/llms.txt](https://docs.kyberswap.com/llms.txt)

[https://docs.kyberswap.com/llms-full.txt](https://docs.kyberswap.com/llms-full.txt)

### Usage

```
# Pull the index
curl -s https://docs.kyberswap.com/llms.txt

# Or paste the URL straight into any AI chat:
#   "Use https://docs.kyberswap.com/llms.txt as context, then …"
```

**Example prompts once llms.txt is loaded:**

* "How do I get a swap quote on Ethereum using the Aggregator API?"
* "Write a script that creates a gasless limit order on BNB Smart Chain."



## Documentation MCP

KyberSwap's documentation site is hosted on GitBook, which automatically generates a read-only MCP server at:

```
https://docs.kyberswap.com/~gitbook/mcp
```

Once connected, your AI assistant can search through the full documentation, retrieve specific pages, and answer questions using real-time content from [docs.kyberswap.com](http://docs.kyberswap.com) — user guides, developer guides, API references, and all other published pages.

This is a **documentation-only** server. It does not execute swaps or build transactions — that is the role of the MCP Server described under _Execute Operations_ below.

### Server URL

```
https://docs.kyberswap.com/~gitbook/mcp
```

HTTP transport. No authentication required. The server only provides access to published content.

### Setup

{% tabs %}
{% tab title="Claude Code" %}
```
claude mcp add --scope user --transport http kyberswap-docs https://docs.kyberswap.com/~gitbook/mcp
```

Verify with:

```
claude mcp list
```


{% endtab %}

{% tab title="Claude Desktop" %}
Go to Settings > Connectors > Add custom connector. Set the name to KyberSwap Docs and the URL to:

<pre><code><strong>https://docs.kyberswap.com/~gitbook/mcp
</strong></code></pre>

When chatting, click the attachments button (plus icon) and select the KyberSwap Docs connector.


{% endtab %}

{% tab title="Cursor" %}
Open the command palette (Cmd + Shift + P / Ctrl + Shift + P), search for **Open MCP settings**, and add:

```
{
  "mcpServers": {
    "kyberswap-docs": {
      "url": "https://docs.kyberswap.com/~gitbook/mcp"
    }
  }
}
```


{% endtab %}

{% tab title="Windsurf" %}
Open the command palette, search for **Windsurf: Configure MCP Servers**, and add:

```
{
  "mcpServers": {
    "kyberswap-docs": {
      "serverUrl": "https://docs.kyberswap.com/~gitbook/mcp"
    }
  }
}
```


{% endtab %}

{% tab title="VS Code" %}
Run from terminal:

```
code --add-mcp '{"name":"kyberswap-docs","type":"http","url":"https://docs.kyberswap.com/~gitbook/mcp"}'
```


{% endtab %}
{% endtabs %}

#### **Other MCP-compatible tools**

Any tool that supports the MCP protocol can connect to [https://docs.kyberswap.com/\~gitbook/mcp](https://docs.kyberswap.com/~gitbook/mcp) using HTTP transport.

### What the agent gets

Once connected, the assistant has real-time access to:

* Search across all published documentation pages.
* Retrieve full page content for any doc, guide, or API reference.
* Answer questions using the latest published content — never drafts or unpublished changes.
