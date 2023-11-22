---
description: Your KyberAI Questions Answered
---

# FAQ

## General

<details>

<summary>What is KyberAI?</summary>

KyberAI was conceived with the intention of surfacing valuable market data that would empower KyberSwap users to make data-driven trades. With KyberAI, users gain access to a wealth of market data that is usually only afforded to institutional traders or high net worth individuals. KyberAI aggregates both [on-chain](on-chain-indicators/) and [off-chain](technical-indicators/) data across [multiple chains](../../getting-started/supported-exchanges-and-networks.md) and condenses this wealth of data into actionable insights which can be conveniently accessed via the [KyberSwap Interface](https://kyberswap.com/discover).&#x20;

Please refer to our [Docs](./) for a complete explanation of KyberAI and how it can be used to supercharge your trades.

</details>

<details>

<summary>What is KyberScore? </summary>

[KyberScore](kyberscore.md) is KyberAI's flagship feature which takes advantage of advancements in AI models to compute a numeric score indicating how bullish or bearish a token is expected to be over the next 24 hours.

Please refer to our [Docs](kyberscore.md) for a complete explanation of KyberScore's design as well as data sources used to train our KyberScore model.

</details>

<details>

<summary>What is the difference between KyberAI and KyberScore?</summary>

While [KyberScore](kyberscore.md) is the flagship feature of [KyberAI](./) which enables users a peek into the token's future price performance, KyberAI comes with many other complementary features. KyberAI also condenses the wealth of on and off-chain token data into easily digestible graphs. Moreover, KyberAI also comes equipped with an [interactive technical analysis component ](technical-indicators/live-charts.md)where advanced traders can combine a myriad of TA tools to evaluate a token based on their specific trading strategy.

In short, KyberScore is another indicator within the KyberAI toolset. This being said, significant effort has been invested to ensure the applicability of the KyberScore model and hence any trading strategy will likely benefit from leveraging the additional insights made possible via KyberScore.

For more details on each, you can refer to our Docs on [KyberAI](./) and [KyberScore](kyberscore.md). This includes all the other [On-Chain Indicators](on-chain-indicators/) and [Technical Indicators](technical-indicators/) that complete the KyberAI feature suite.

</details>

<details>

<summary>Which chains do KyberAI currently support?</summary>

KyberAI currently supports more than 4000 tokens deployed across the following 7 chains:

* Ethereum (ChainID: 1)
* BSC (ChainID: 56)
* Arbitrum (ChainID: 42161)
* Polygon PoS (ChainID: 137)
* Optimism (ChainID: 10)
* Fantom (ChainID: 250)
* Avalanche (ChainID: 43114)

</details>

<details>

<summary>How updated is KyberAI data?</summary>

KyberAI always strives to display the most updated data for our users. Given the abundance of data points being queried, the data refresh rate is specific to a particular indicator. Data liveness has been optimized to account for the type of data as well as the practicality of computing said data.

You can refer to the Data Sources section of each indicator for the refresh rate used for the specific indicator. For your convenience, below is a summary of KyberAI refresh rates across various data sets:

* [**Token Rankings**](user-guides/discover-promising-tokens.md): Every 4 hours
* [**KyberScore**](kyberscore.md): Every hour
* [**Number Of Trades**](on-chain-indicators/number-of-trades.md): Every hour
* [**Trading Volume**](on-chain-indicators/trading-volume.md): Every hour
* [**Netflow To Whale Wallets**](on-chain-indicators/netflow-to-whale-wallets.md): Every hour
* [**Netflow To CEX**](on-chain-indicators/netflow-to-cex.md): Every hour
* [**Number Of Transfers**](on-chain-indicators/number-of-transfers.md): Every hour
* [**Volume Of Transfers**](on-chain-indicators/volume-of-transfers.md): Every hour
* [**Number Of Holders**](on-chain-indicators/number-of-holders.md): Every 24 hours
* [**Top Holders**](on-chain-indicators/top-holders.md): Every 24 hours
* [**Live Charts**](technical-indicators/live-charts.md): Price is refreshed every minute with OHLCV data refreshed every 5 minutes
* [**Support & Resistance Levels**](technical-indicators/support-and-resistance-levels.md): Every hour
* [**Live Trades**](technical-indicators/live-trades.md): Refrehsed every 10 seconds with a 2 minute lag
* [**Funding Rate On CEX**](technical-indicators/funding-rate-on-cex.md): Every hour
* [**Liquidations On CEX**](technical-indicators/liquidations-on-cex.md): Every hour
* **KyberAI Token List**: Every 2 weeks
* **Whale Wallet List**: Every 2 weeks

</details>

<details>

<summary>Are there API Endpoints for KyberAI?</summary>

KyberAI was developed for the benefit and convenience of KyberSwap users and are intended to help our users make informed decisions about trading on our platform.

As such, we do not have any public-facing API endpoints, and we do not currently have any plans to make this feature available outside of the KyberSwap platform.

</details>

<details>

<summary>What is an on-chain indicator?</summary>

On-chain indicators make use of data that is stored on publicly accessible blockchains. Unlike the traditional Web2 model whereby data is stored on a private database, on-chain data can be accessed by anyone and does not require a trusted API to be implemented by the service provider for data to be queried in a trusted manner.

For the majority of actions that occurs in DeFi, an event of the transaction will be logged onto the blockchain which can then be publicly queried. Some examples of on-chain data includes DEX swaps, token transfers, addresses holding the token, and many others.

Please refer to [On-Chain vs Off-Chain Data](../../getting-started/foundational-topics/decentralized-technologies/on-chain-vs-off-chain-data.md) for a more in-depth comparison of on-chain vs off-chain data sources.

</details>

<details>

<summary>What is the difference between Trending and Trending Soon?</summary>

The **Trending** and **Trending Soon** rankings on [KyberSwap.com](http://kyberswap.com/) are tools developed by KyberSwap to allow you to see trading trends in DeFi, helping you to trade efficiently.

### Trending

Tokens displayed on the Trending table are based on current data gleaned from top data aggregators such as CoinGecko and Coinmarketcap.

### Trending Soon

Tokens displayed on the Trending Soon table are detected based on our Trend detection algorithm, using trading volume, price, market cap and other on-chain data. These tokens may not be trending _now_, but could very well be trending soon.

Please refer to [Discover Promising Tokens](user-guides/discover-promising-tokens.md) for a full overview of the various ranking features.

</details>

## Access

<details>

<summary>How do I get access to KyberAI?</summary>

KyberAI is currently undergoing its beta testing phase whereby access is granted to our most active and influential KyberSwap community members. This staged rollout ensures that KyberAI can continue to be improved following targeted feedback from an initial set of key community users.

As we move towards a public rollout for KyberAI, do keep a lookout for announcements across various social channels which will enable you to join the KyberAI waitlist during this testing period. Please refer to [Sign In To KyberAI With Ethereum](user-guides/sign-in-to-kyberai-with-ethereum.md) for further details on the registration process.

</details>

<details>

<summary>Why do I need to connect my email to use KyberAI?</summary>

KyberAI was created with the intention of democratizing trading insights for all hence all of KyberAI's features are accessible to anyone with an Ethereum wallet. As KyberAI is rolled out to the public, it will undergo multiple rounds of beta testing to garner further feedback from our most active ecosystem members. This ensures that, at the point of public release, the data insights made available via KyberAI will drive significant value-add to any trading strategy right off the bat.

Leveraging upon the amazing work of [Sign-In With Ethereum](https://docs.login.xyz/), KyberAI users will now be able to sign into the KyberAI interface using their Ethereum wallets. By validating the selected EVM address against a preferred email address, no personally identifiable information needs to be shared with KyberSwap in order to utilize KyberAI trading insights. The linked email will only be used for the purposes of endorsing users as well as for communications.

</details>

<details>

<summary>Can I connect more than 1 address to my email?</summary>

Yes, you can reuse the same email when registering your connected wallet address. For every address linked, it will have to go through the same waitlist process as detailed in [Sign In To KyberAI With Ethereum](user-guides/sign-in-to-kyberai-with-ethereum.md).

</details>

## Troubleshooting

<details>

<summary>I'm unable to find my token on KyberAI</summary>

While KyberAI enables data to be surfaced for any ERC20 token, our model requires that the token generates a target trade volume as well as have at least 37 days of token data available before it can be added to the KyberAI catalog. Aside from ensuring the consistency of data displayed on KyberAI, this requirement also functions as a safeguard against less established tokens whose credibility has yet to be demonstrated.

The list of tokens that meet the KyberAI qualification criteria will be refreshed every two weeks. At this point, KyberAI will scan various on and off-chain data points to determine a token's eligibility. Note that tokens can be added or removed from this list depending on the overall interest in the token.

</details>

<details>

<summary> Will I still be able to see data for tokens which has been removed from KyberAI?</summary>

KyberAI constantly refreshes its list of eligible tokens to ensure that the data shown is always as accurate as possible. For tokens which have previously been added to KyberAI, you will be able to view the token's data as long as the token has been added to your watchlist when it was active on KyberAI.&#x20;

</details>

Still can't find what you're looking for? Check out the [KyberSwap Help Center](https://support.kyberswap.com/hc/en-us).
