---
description: >-
  The @kyberswap/liquidity-widgets package is an npm package of React components
  used to provide subsets of the Zap Protocol functionality in a small and
  configurable user interface element.
---

# Integrating The KyberSwap Liquidity Widget

Demo: [https://kyberswap.com/earn](https://kyberswap.com/earn)

Installing the Liquidity Widget

To get started, install the widgets library using npm or Yarn.

{% embed url="https://www.npmjs.com/package/@kyberswap/liquidity-widgets" %}

**npm:**

```
npm i @kyberswap/widgets
```

**Yarn:**

```
yarn add @kyberswap/widgets
```

## Adding the Liquidity widget to your app

Embed the React component in your application with this piece of code:

```javascript
import "@kyberswap/liquidity-widgets/dist/style.css";
import { LiquidityWidget, PoolType } from "@kyberswap/liquidity-widgets";

<LiquidityWidget
  theme={{
    text: "#FFFFFF",
    subText: "#B6AECF",
    icons: "#a9a9a9",
    layer1: "#27262C",
    dialog: "#27262C",
    layer2: "#363046",
    stroke: "#363046",
    chartRange: "#5DC5D2",
    chartArea: "#457F89",
    accent: "#5DC5D2",
    warning: "#F4B452",
    error: "#FF5353",
    success: "#189470",
    fontFamily: "Kanit, Sans-serif",
    borderRadius: "20px",
    buttonRadius: "16px",
    boxShadow: "0px 4px 4px rgba(0, 0, 0, 0.04)",
  }}
  poolType={PoolType.DEX_UNISWAP_V4_FAIRFLOW}
  poolAddress="0x1508630c3e36bf8b524db0fc321565bef8aece8bc1c706ed7ac9a88b9657a6c0"
  chainId={1}
  connectedAccount={{
    address: "0xa6c883E2dde82FbED20e025BD717a6B7F34f5E6E", 
    chainId: 56
  }}
  onClose={() => {
    console.log("Close Widget");
  }}
  onConnectWallet={() => {
    // trigger your connect wallet here
  }}
  onSwitchChain={() => {
    // handle change network if connectedAccount.chainId != chainId
  }}
  onSubmitTx={(txData: {from: string, to: string, value: string, data: string, gasLimit: string}}) => {
    // Submit your transaction to wallet 
  }}
  source="zap-widget-demo"
/>

```

## Liquidity Widget Props

<table><thead><tr><th width="167.57208251953125">Property</th><th width="305.3994140625">Description</th><th width="131.80126953125">Type</th><th>Default Value</th></tr></thead><tbody><tr><td>theme</td><td>Customize theme for Liquidity Widget</td><td>Theme</td><td><a href="https://github.com/KyberNetwork/kyberswap-widgets/blob/main/packages/liquidity-widgets/src/theme/index.ts#L1-L19">defaultTheme</a></td></tr><tr><td><del>provider</del></td><td><del>Web3Provider to interact with blockchain</del></td><td><a href="https://docs.ethers.org/v5/api/providers/"><del>Web3Provider</del></a> <del>| undefined</del></td><td><del>undefined</del></td></tr><tr><td>poolAddress</td><td><mark style="color:red;">Required</mark>. Address of pool to zap</td><td>Address</td><td>--</td></tr><tr><td>poolType</td><td><mark style="color:red;">Required.</mark> Type of Pool, supported protocol</td><td><a href="https://github.com/KyberNetwork/kyberswap-widgets/blob/main/packages/liquidity-widgets/src/schema/index.ts#L20-L47">Enum</a></td><td>--</td></tr><tr><td>positionId</td><td>Optional, in case “Increasing Liquidity into an existing position”, pass the position id. The position should belong to the <strong>poolAddress</strong>. Otherwise, it considers as “Adding Liquidity into a new position”</td><td>String | undefined</td><td>undefined</td></tr><tr><td>chainId</td><td><mark style="color:red;">Required.</mark> Network of selected pool.</td><td>number</td><td>--</td></tr><tr><td>connectedAccount </td><td><mark style="color:red;">Required.</mark> The current network that user connected. If not connected, the address should be undefined</td><td>{ address?: string, chainId: number }</td><td>--</td></tr><tr><td>source</td><td><mark style="color:red;">Required.</mark> To identify the dapp that integrates with the iquidity widget</td><td>string</td><td>--</td></tr><tr><td>feeAddress</td><td>Optional, Wallet Address if you want to charge zap fee</td><td>Address</td><td>--</td></tr><tr><td>feePcm</td><td>fee percentage in per cent mille (0.001% or 1 in 100,000). Ignored if feeAddress is empty. From 0 to 100,000 inclusively. Example: 1 for 0.001%.</td><td>number</td><td>--</td></tr><tr><td>includedSources</td><td>List of liquidty sources you want to includes from your zap, separate by comma</td><td><a href="https://docs.kyberswap.com/kyberswap-solutions/kyberswap-aggregator/dex-ids">KyberSwap Aggregator Dex ID</a></td><td>--</td></tr><tr><td>excludedSources</td><td>List of liquidity sources that you want to exclude from your zap, separate by comma</td><td><a href="https://docs.kyberswap.com/kyberswap-solutions/kyberswap-aggregator/dex-ids">KyberSwap Aggregator Dex ID</a></td><td>--</td></tr><tr><td>onClose</td><td>Callback function when click cancel or close widget</td><td>() => void</td><td>--</td></tr><tr><td>onConnectWallet</td><td>action to trigger connect wallet</td><td>() => void</td><td></td></tr><tr><td>onSwitchChain</td><td>action to trigger switch chain if network of the pool is different with network from connected account</td><td>() => void</td><td></td></tr><tr><td>onSubmitTx</td><td>trigger submit transaction (approval or zap). Should return the tx hash</td><td>(txData: {from: string, to: string, value: string, data: string, gasLimit: string}) => Promise</td><td></td></tr><tr><td><del>onTxSubmit</del></td><td><del>Callback function when tx was submited</del></td><td><del>(txHash: string) => void</del></td><td>--</td></tr></tbody></table>

### Migrate from version 0.0.16 to 1.x.x

Deprecated

| Property       | Description                                  | Type                                                      | Default Value |
| -------------- | -------------------------------------------- | --------------------------------------------------------- | ------------- |
| ~~provider~~   | ~~Web3Provider to interact with blockchain~~ | [Web3Provider](https://docs.ethers.org/v5/api/providers/) | undefined     |
| ~~onTxSubmit~~ | ~~Callback function when tx was submitted~~  | (txHash: string) => void                                  |               |

#### New

| Property         | Description                                               | Type                                                                                           | Default Value |
| ---------------- | --------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ------------- |
| connectedAccount | Info of current account that user connect to your website | { address?: string, chainId: number }                                                          |               |
| onTxSubmit       | Function that trigger tx                                  | (txData: {from: string, to: string, value: string, data: string, gasLimit: string}) => Promise |               |
