# Developer Guides

## Overview

The guides in the following section provides a step-by-step walkthrough of Elastic swap and liquidity management operations in a TypeScript environment. For the sake of simplicity, the examples have been implemented purely in Node.js allowing readers to focus on just the operational logic.

Note that all values returned from the Elastic smart contracts are logged into the developer console for troubleshooting and feedback.

{% hint style="warning" %}
**Implemented on Polygon PoS**

The demos have been implemented on Polygon PoS (ChainId: 137) which enables live interactions with production Elastic smart contracts. This means that the information returned is in real-time and write operations uses **real tokens with monetary value**.

While this provides the best learning environment without the overhead of setting up a complete test environment, users are advised to practice additional caution when executing the scripts.
{% endhint %}

### Trade

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="get-a-quote.md"><strong>Get A Quote</strong></a></td><td></td><td></td><td><a href="get-a-quote.md">get-a-quote.md</a></td></tr><tr><td><strong>Execute A Trade</strong></td><td></td><td></td><td></td></tr></tbody></table>

### Liquidity Management

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><strong>Create New Position</strong></td><td></td><td></td></tr><tr><td><strong>Increase Liquidity</strong></td><td></td><td></td></tr><tr><td><strong>Remove Liquidity</strong></td><td></td><td></td></tr><tr><td><strong>Collect Trading Fees</strong></td><td></td><td></td></tr></tbody></table>

## NPM Packages

### KyberSwap Elastic SDK package

```
npm i @kyberswap/ks-sdk-elastic
```

{% embed url="https://www.npmjs.com/package/@kyberswap/ks-sdk-elastic" %}

### KyberSwap Core SDK package

```
npm i @kyberswap/ks-sdk-core
```

{% embed url="https://www.npmjs.com/package/@kyberswap/ks-sdk-core" %}
