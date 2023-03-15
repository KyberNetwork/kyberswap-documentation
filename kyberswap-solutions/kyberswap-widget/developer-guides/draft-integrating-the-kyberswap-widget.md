---
description: The Best Rates With Minimal Code
---

# Integrating The KyberSwap Widget

## Installing the Swap Widget

To get started, install the widgets library using npm or Yarn.

#### npm:[​](https://docs.kyberswap.com/Aggregator/swap-widget/getting-started#npm) <a href="#npm" id="npm"></a>

```
npm i @kyberswap/widgets
```

#### yarn:[​](https://docs.kyberswap.com/Aggregator/swap-widget/getting-started#yarn) <a href="#yarn" id="yarn"></a>

```
yarn add @kyberswap/widgets
```

## Adding the Swap widget to your app

Embed the React component in your application with this piece of code:

```
import { Widget } from "@kyberswap/widgets";

<Widget
    theme={theme}
    tokenList={[]}
    provider={ethersProvider}
    defaultTokenOut={defaultTokenOut[chainId]}
/>
```

That's it! You should now see a fully functional swap widget on your site. You can easily [customize the widget](customizing-the-kyberswap-widget.md) according to your application colors.
