---
description: Code Samples To Get You Started
---

# Developer Guides

The guides in the following section are targeted at application developers as well as smart contract integrators that are interested in building on top of the KyberSwap Aggregator ecosystem.

## Overview

To cater for varying integration complexities, KyberSwap Aggregator offers developers 2 options for integration:

* [**KyberSwap Widget**](../../kyberswap-widget/): An endlessly customizable widget that can be seamlessly integrated with a few lines of code. Refer to [Integrating The KyberSwap Widget](../../kyberswap-widget/developer-guides/integrating-the-kyberswap-widget.md) for instructions on how to install and add the widget to your frontend.
* [**Aggregator API**](../aggregator-api-specification/): For developers that require more fine-tuned control when integrating swap functionality within their app. If you're just getting started with the KyberSwap Aggregator, you can refer to our [Execute A Swap With The Aggregator API](execute-a-swap-with-the-aggregator-api.md) dev guide for information and code samples on how to query and execute swaps at the favourable rates.

{% hint style="info" %}
#### KyberSwap Aggregator APIv1 Upgrades

The [EVM swap](../aggregator-api-specification/evm-swaps.md) API has been upgraded for more performant queries and the details behind the enhancement as well as the updated swap flows can be viewed on [Upgrading To APIv1](upgrading-to-apiv1.md).
{% endhint %}

KyberSwap Aggregator implements a router contract which handles the complexity of routing and executing swaps atomically. Please refer to [Aggregator Contract Addresses](../contracts/aggregator-contract-addresses.md) for the full list of contracts which have been deployed across the supported chains.

## Next steps

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="execute-a-swap-with-the-aggregator-api.md"><strong>Execute A Swap With The Aggregator API</strong></a></td><td></td><td></td><td><a href="execute-a-swap-with-the-aggregator-api.md">execute-a-swap-with-the-aggregator-api.md</a></td></tr><tr><td><a href="broken-reference"><strong>Plug And Play The KyberSwap Widget</strong></a></td><td></td><td></td><td><a href="broken-reference">Broken link</a></td></tr><tr><td><a href="../../kyberswap-widget/developer-guides/customizing-the-kyberswap-widget.md"><strong>Customize The KyberSwap Widget</strong></a></td><td></td><td></td><td><a href="../../kyberswap-widget/developer-guides/customizing-the-kyberswap-widget.md">customizing-the-kyberswap-widget.md</a></td></tr><tr><td><a href="broken-reference"><strong>More Performant Queries With APIv2</strong></a></td><td></td><td></td><td><a href="broken-reference">Broken link</a></td></tr></tbody></table>
