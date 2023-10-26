---
description: Superior Rates With Minimal Code
---

# Integrating The KyberSwap Widget

## Installing the Swap Widget

To get started, install the widgets library using npm or Yarn.

#### npm:[​](https://docs.kyberswap.com/Aggregator/swap-widget/getting-started#npm) <a href="#npm" id="npm"></a>

```
npm i @kyberswap/widgets
```

{% embed url="https://www.npmjs.com/package/@kyberswap/widgets" %}

#### yarn:[​](https://docs.kyberswap.com/Aggregator/swap-widget/getting-started#yarn) <a href="#yarn" id="yarn"></a>

```
yarn add @kyberswap/widgets
```

## Adding the Swap widget to your app

{% hint style="success" %}
#### Note on integrations: clientID

In order to continuously improve the KyberSwap Widget, our widget implements a `client` field that enables us to understand how the widget swaps are being utilized. As a developer integrating with our widget, **please add your clientID (i.e. company name) to the `client` field** to enable us to serve you better. Refer below for example.
{% endhint %}

Embed the React component in your application with this piece of code:

```
import { Widget } from "@kyberswap/widgets";

<Widget
    client="yourCompanyNameHere"
    theme={theme}
    tokenList={[]}
    enableRoute = true
    enableDexes="kyberswap-elastic,uniswapv3,uniswap"
    provider={ethersProvider}
    defaultTokenOut={defaultTokenOut[chainId]}
    title={<div>Custom Title</div>}
/>
```

That's it! You should now see a fully functional swap widget on your site. You can easily [customize the widget](customizing-the-kyberswap-widget.md) according to your application colors.
