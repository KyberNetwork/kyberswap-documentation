---
description: Endlessly Customizable
---

# Customizing The KyberSwap Widget

## Overview

Below you’ll find a few examples showing how you can [customize the widget theme](https://docs.kyberswap.com/Aggregator/swap-widget/customize-widget) to match the look and feel of your dApp. All of them can be integrated using the following code snippet where you can set your `theme`:

```javascript
import { Widget } from "@kyberswap/widgets";

const theme: Theme = {
  // Check out the theme examples below
}

<Widget
  client="yourCompanyNameHere"
  theme={theme}
  tokenList={[]}
  provider={ethersProvider}
  defaultTokenOut={defaultTokenOut[chainId]}
/>
```

## Customizing the title

Integrators are free to set their own widget title using ReactNode or just a `string` value.

```javascript
  import { Widget } from "@kyberswap/widgets";

  <Widget
    title={
      <div>Custom Title</div>
    }
  />
```

## Customizing the width

Widget has a fixed height of 360px and a default width of 360px. You cannot modify the height of the widget. You can modify the width up to a minimum width of 300px.

You can customize the width by passing a valid CSS number or width to the widget's width holder.

```javascript
  import { Widget } from "@kyberswap/widgets";

  <Widget
    width={360}
  />
```

## Customizing the fees

The KyberSwap Widget makes it easy to configure a transaction facilitation fee by passing additional parameters to the widget. Information about parameters you can refer to [KyberSwap Aggregator APIs](../../kyberswap-aggregator/aggregator-api-specification/evm-swaps.md).

```javascript
import { Widget } from "@kyberswap/widgets";

<Widget  feeSetting={
    feeAmount: 100,
    feeReceiver: "0xDcFCD5dD752492b95ac8C1964C83F992e7e39FA9",
    chargeFeeBy: "currency_in",
    isInBps: true,
} />
```

## Customizing the themes

You can set optional parameters to tailor the appearance and functionality of the swap widget to fit your app.

All attributes below are color codes, except `buttonRadius` (number), `borderRadius` (number between 0 and 1), and `fontFamily` (string).

You can check out examples of the swap widget, and the [Figma](https://www.figma.com/file/xXVDyWzLPrJgzrQ4GMroRp/Kyber-Widget?node-id=1%3A2) file if you want to mock it up first!

![Widget](https://docs.kyberswap.com/assets/images/darkmode-4d3902ec1c47620fdefd19b3d3722f71.png)

<table><thead><tr><th width="206">Properties</th><th width="161">Prop Type</th><th width="149">Example</th><th>Description</th></tr></thead><tbody><tr><td><code>primary</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>primary background color of swap form</td></tr><tr><td><code>secondary</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>secondary background color of swap form</td></tr><tr><td><code>dialog</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>color of dialog</td></tr><tr><td><code>borderRadius</code></td><td><code>string</code></td><td><code>30px</code></td><td>border-radius of swap form and swap button (same border-radius)</td></tr><tr><td><code>buttonRadius</code></td><td><code>string</code></td><td><code>5px</code></td><td>border-radius of swap button</td></tr><tr><td><code>stroke</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>color of the stroke</td></tr><tr><td><code>interactive</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>color of interactive button(Swap icon and token picker)</td></tr><tr><td><code>accent</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>swap button and link color</td></tr><tr><td><code>success</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>success color</td></tr><tr><td><code>warning</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>warning color</td></tr><tr><td><code>error</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>error color</td></tr><tr><td><code>text</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>primary text color</td></tr><tr><td><code>subtext</code></td><td><code>string</code></td><td><code>#F1FFEE</code></td><td>secondary text color</td></tr><tr><td><code>fontFamily</code></td><td><code>string</code></td><td><code>Roboto</code></td><td>font-family of Swap form</td></tr></tbody></table>

## Customizing the Trade Route

The KyberSwap Widget can be configured to also return the trade route by setting the `enableRoute` parameter to `true`.

Moreover, you can also specify the list of DEXs which trades via the widget will be routed to using the `enableDexes` parameter. The full list of DEX IDs can be found [here](../../kyberswap-aggregator/dex-ids.md).

## Customizing the Token Lists

```javascript
import { Widget } from "@kyberswap/widgets";

// You can also pass a list of tokens as JSON, as long as the format is correct
const MY_TOKEN_LIST = [
    {
    "name": "KNC",
    "address": "0x1C954E8fe737F99f68Fa1CCda3e51ebDB291948C",
    "symbol": "KNC",
    "decimals": 18,
    "chainId": 1,
    "logoURI": "https://s2.coinmarketcap.com/static/img/coins/64x64/9444.png"
  },
    {
    "name": "Tether USD",
    "address": "0xdAC17F958D2ee523a2206206994597C13D831ec7",
    "symbol": "USDT",
    "decimals": 6,
    "chainId": 1,
    "logoURI": "https://raw.githubusercontent.com/trustwallet/assets/master/blockchains/ethereum/assets/0xdAC17F958D2ee523a2206206994597C13D831ec7/logo.png"
  },
  {
    "name": "USD Coin",
    "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
    "symbol": "USDC",
    "decimals": 6,
    "chainId": 1,
    "logoURI": "https://raw.githubusercontent.com/trustwallet/assets/master/blockchains/ethereum/assets/0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48/logo.png"
  },
]

<Widget
    theme={theme}
    tokenList={MY_TOKEN_LIST}
    provider={ethersProvider}
    defaultTokenOut={defaultTokenOut[chainId]}
/>
```
