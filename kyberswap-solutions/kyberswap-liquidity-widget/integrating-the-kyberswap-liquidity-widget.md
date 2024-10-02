---
description: Zap into a Liquidity Protocol With Minimal Code
---

# Integrating The KyberSwap Liquidity Widget

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
import { LiquidityWidget } from "@kyberswap/liquidity-widgets";

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
  provider={ethersProvider}
  chainId={56}
  poolType={PoolType.DEX_PANCAKESWAPV3}
  poolAddress="0x36696169c63e42cd08ce11f5deebbcebae652050"
  onDismiss={() => {
    console.log("Dismiss");
  }}
  source="zap-widget-demo"
/>

```



## Liquidity Widget Props

<table><thead><tr><th width="144">Property</th><th width="215">Description</th><th width="175">Type</th><th>Default Value</th></tr></thead><tbody><tr><td>theme</td><td>Customize theme for Liquidity Widget</td><td>Theme</td><td><a href="https://github.com/KyberNetwork/kyberswap-widgets/blob/main/packages/liquidity-widgets/src/theme/index.ts#L1-L19">defaultTheme</a></td></tr><tr><td>provider</td><td>Web3Provider to interact with blockchain</td><td><a href="https://docs.ethers.org/v5/api/providers/">Web3Provider</a> | undefined</td><td>undefined</td></tr><tr><td>chainId</td><td><mark style="color:red;">Required.</mark> A unique identifier that represents a blockchain network. </td><td>number</td><td>--</td></tr><tr><td>poolAddress</td><td><mark style="color:red;">Required</mark>. SmartContract address of pool</td><td>Address</td><td>--</td></tr><tr><td>poolType</td><td><mark style="color:red;">Required.</mark> Type of Pool</td><td>enum</td><td><p></p><ul><li>DEX_UNISWAPV3</li><li>DEX_PANCAKESWAPV3</li></ul></td></tr><tr><td>positionId</td><td>Optional, in case “Increasing Liquidity into an existing position”, pass the position id. The position should belong to the <strong>poolAddress</strong>. Otherwise, it considers as “Adding Liquidity into a new position”</td><td>String | undefined</td><td>undefined</td></tr><tr><td>source</td><td><mark style="color:red;">Required.</mark> To identify the dapp that integrating with liquidity widget</td><td>string</td><td>--</td></tr><tr><td>feeAddress</td><td>Optional, Wallet Address if you want to charge zap fee</td><td>Address</td><td>--</td></tr><tr><td>feePcm</td><td>fee percentage in per cent mille (0.001% or 1 in 100,000). Ignored if feeAddress is empty. From 0 to 100,000 inclusively. Example: 1 for 0.001%.</td><td>number</td><td>--</td></tr><tr><td>includedSources</td><td>List of liquidty sources you want to includes from your zap, separate by comma</td><td><a href="https://docs.kyberswap.com/kyberswap-solutions/kyberswap-aggregator/dex-ids">KyberSwap Aggregator Dex ID</a></td><td>--</td></tr><tr><td>excludedSources</td><td>List of liquidity sources that you want to exclude from your zap, separate by comma</td><td><a href="https://docs.kyberswap.com/kyberswap-solutions/kyberswap-aggregator/dex-ids">KyberSwap Aggregator Dex ID</a></td><td>--</td></tr><tr><td>onDismiss</td><td>Callback function when click cancel or close widget</td><td>() => void</td><td>--</td></tr><tr><td>onTxSubmit</td><td>Callback function when tx was submited </td><td>(txHash: string) => void</td><td>--</td></tr></tbody></table>
