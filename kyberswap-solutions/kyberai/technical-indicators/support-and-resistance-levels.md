# Support & Resistance Levels

{% hint style="info" %}
#### In one sentence

Psychological price levels which limits the range of market movement based on the min/max value assigned by the market for an arbitrary time period.
{% endhint %}

## Overview

Support and resistance levels are two terms that are used in technical analysis to identify when traders expect further price movements in a particular direction to be limited (i.e. a price reversal). As per its namesake, a support level indicates that the market is currently "supporting" a particular price level which limits further downward price movements. On the other hand, a resistance level indicates that the market is currently "resisting" a particular price level which limits further upward price movements. When demand greatly outstrips supply at a specific price, that price becomes a support level whereas if supply greatly outstrips demand at a specific price, that price becomes a resistance level. As such, the "level" refers to the price level which could then become a support or resistance level depending on the market's direction.

<figure><img src="../../../.gitbook/assets/image (167).png" alt=""><figcaption><p>Identified support &#x26; resistance levels</p></figcaption></figure>

Support and resistance levels are a natural outcome of the market as individual traders collectively try to predict when an asset is over or undervalued. Consequently, these price levels act as self-perpetuating psychological barriers for traders as whenever an asset's price approaches these levels, traders are inclined to buy or sell based on the expectation that other traders will buy or sell around the same price level. As such, the more times an asset's price approaches a level only to bounce back in the opposite direction, the stronger the psychological barrier resulting in greater correlation between future price movements and the identified price level. This effect is accentuated even further whenever the price breaks through the level only to immediately fall back to the level (i.e. testing the level).

Given that the support level limits downwards movements while the resistance level limits upwards movements, these levels form a range within which the market tends to trade. Without any significant breaks outside these price levels, market movements will likely continue to be bounded between the support and resistance level. Whenever the price breaks through a price level for a prolonged period of time, the price will likely continue its movement in the same direction until the market settles on a new support and resistance level. Recall that these levels are effectively psychological and hence time becomes a significant factor when establishing such levels.

## Improving trades with Support & Resistance levels

{% hint style="warning" %}
#### Disclaimer: Not financial advice

KyberAI was created with the intention of empowering our users with the data insights required to make informed trading decisions. Users must exercise due diligence in their trading decisions with the best trading strategies incorporating the insights enabled by KyberAI.
{% endhint %}

For an identified support level, you can expect the downward price movement to reverse upon approaching the support level. On the other hand, for an identified resistance level, you can expect the upward price movement to reverse upon approaching the resistance level. The longer the price is unable to breakthrough the identified price level, the stronger the psychological barrier attached to that price level. Once a price level has been broken for a significant amount of time, the market will likely continue moving in that direction until a new support/resistance level is found.

## Data source(s)

{% tabs %}
{% tab title="CoinMarketCap" %}
**API**: [https://pro-api.coinmarketcap.com](https://pro-api.coinmarketcap.com)

* /v2/cryptocurrency/quotes/historical
{% endtab %}

{% tab title="CoinGecko" %}
**API**: [https://pro-api.coingecko.com/api](https://pro-api.coingecko.com/api)

* /v3/coins/{token\_id}/market\_chart/range
{% endtab %}
{% endtabs %}

Computed based on data from CoinMarketCap and CoinGecko. Data is refreshed every hour.
