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
theme={theme}
tokenList={[]}
provider={ethersProvider}
defaultTokenOut={defaultTokenOut[chainId]}
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

<Widget  feeSetting={{
    feeAmount: 100,
    feeReceiver: "0xDcFCD5dD752492b95ac8C1964C83F992e7e39FA9",
    chargeFeeBy: "currency_in",
    isInBps: true,
}} />
```

## Customizing the themes

You can set optional parameters to tailor the appearance and functionality of the swap widget to fit your app.

All attributes below are color codes, except `buttonRadius` (number), `borderRadius` (number between 0 and 1), and `fontFamily` (string).

You can check out examples of the swap widget, and the [Figma](https://www.figma.com/file/xXVDyWzLPrJgzrQ4GMroRp/Kyber-Widget?node-id=1%3A2) file if you want to mock it up first!

![Widget](https://docs.kyberswap.com/assets/images/darkmode-4d3902ec1c47620fdefd19b3d3722f71.png)

| Properties     | Prop Type | Example   | Description                                                     |
| -------------- | --------- | --------- | --------------------------------------------------------------- |
| `primary`      | `string`  | `#F1FFEE` | primary background color of swap form                           |
| `secondary`    | `string`  | `#F1FFEE` | secondary background color of swap form                         |
| `dialog`       | `string`  | `#F1FFEE` | color of dialog                                                 |
| `borderRadius` | `string`  | `30px`    | border-radius of swap form and swap button (same border-radius) |
| `buttonRadius` | `string`  | `5px`     | border-radius of swap button                                    |
| `stroke`       | `string`  | `#F1FFEE` | color of the stroke                                             |
| `interactive`  | `string`  | `#F1FFEE` | color of interactive button(Swap icon and token picker)         |
| `accent`       | `string`  | `#F1FFEE` | swap button and link color                                      |
| `success`      | `string`  | `#F1FFEE` | success color                                                   |
| `warning`      | `string`  | `#F1FFEE` | warning color                                                   |
| `error`        | `string`  | `#F1FFEE` | error color                                                     |
| `text`         | `string`  | `#F1FFEE` | primary text color                                              |
| `subtext`      | `string`  | `#F1FFEE` | secondary text color                                            |
| `fontFamily`   | `string`  | `Roboto`  | font-family of Swap form                                        |

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
