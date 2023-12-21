---
description: Digital Representation Of Value
---

# Tokens

## What is a token?

Tokens are essentially digital representation of assets on the blockchain. This can be blockchain native assets where the asset is fully described by the blockchain or a tokenised representation of an asset that is external to the blockchain. In the latter case, an [oracle](https://ethereum.org/en/developers/docs/oracles/) or trusted party is required to bridge the asset into the blockchain. Note that tokens can represent anything and everything as it is just tokenised data.

## Coins vs Tokens

While everything can be tokenized on the blockchain, it is important to differentiate between coins and tokens so that you don't end up with frozen funds.

* Coins are essentially a form of digital currency which is native to its blockchain. The blockchain protocol defines the coins supply curve which includes the minting and burning of coins.\
  \
  Coins facilitate activity on the chain by creating a market for on-chain computing resources. The easiest method to identify a coin is if a blockchain requires you to pay transaction fees denominated in their native coin. \
  \
  Below are the list of blockchains and their respective coins which are supported by KyberSwap. Do note that each chain has control over their coin symbol and as such some chains have opted to keep the ETH symbol. The ETH coin is specific to each chain and are not interoperable. You can refer to [Bridge Your Assets Across Multiple Chains](broken-reference) if you would like to transfer coin value form one chain to the next.

| Blockchain       | Coin Symbol |
| ---------------- | ----------- |
| Ethereum         | ETH         |
| BNB Smart Chain  | BNB         |
| Arbitrum         | ETH         |
| Polygon PoS      | MATIC       |
| Optimism         | OP          |
| Avalanche        | AVAX        |
| Base             | ETH         |
| Cronos           | CRO         |
| zkSync Era       | ETH         |
| Fantom           | FTM         |
| Linea            | ETH         |
| Polygon zkEVM    | ETH         |
| Aurora           | ETH         |
| BitTorrent Chain | BTT         |
| Scroll           | ETH         |

* Tokens do not have their own blockchain and instead leverages existing chains (each with their own coins) to create and store their token data. Token teams are able to define the token supply and behaviour by creating a token [smart contract](https://ethereum.org/en/smart-contracts/) that is hosted on a blockchain. Consequently, token economics (a.k.a. tokenomics) can be specially crafted to suit a particular use case on the chain.\
  \
  The use cases for tokens are only limited by code. As such, token applications are virtually unlimited. Some popular use cases are: utility tokens to use a particular service, governance tokens that enable holders to participate in project governance, non-fungible tokens to prove exclusive ownership.\
  \
  The same token ticker can exist on multiple chains depending on which chains the token smart contract has been deployed on. While the token conceptually represents the same asset across chains, you will still need to [bridge](broken-reference) the token to your selected chain if you are performing any actions on that chain.

## Token standards

As tokens are effectively on-chain data, token standards were sorely needed as the crypto space matured. Such standards ensured that each token implemented a standard set of fields and functions that made them interoperable with other tokens. Moreover, this set the foundation for a whole range of services which enabled value to be seamlessly transferred across distinct applications.

The two most popular token standards that established itself in the DeFi space are:

* [ERC20](https://docs.openzeppelin.com/contracts/4.x/erc20): A standard for fungible tokens which implements a basic set of token characteristics including name, symbol, and decimals. This is supplemented with additional functionalities which enable developers to mint/burn/transfer tokens as well as query token balances.
* [ERC721](https://docs.openzeppelin.com/contracts/4.x/erc721): A standard for non-fungible tokens (NFTs) which implements a basic set of characteristics including collection name, symbol, and NFT identifiers. In addition to the ERC20 functionalities, ERC721 also adds further functionalities that enables querying of NFT owners.

## Trade and earn with your preferred stablecoins&#x20;

KyberSwap supports the trading of any token that implements the ERC20 standard. You can [Add Your Favourite Tokens](../../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md) via the KyberSwap interface and start trading them immediately.

{% tabs %}
{% tab title="Traders" %}
* [Add Your Favourite Tokens](../../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md)
* [Instantly Swap At Superior Rates](broken-reference)
* [Swap At Your Preferred Rates](../../../kyberswap-solutions/kyberswap-interface/user-guides/trade-at-your-preferred-rates.md)
{% endtab %}

{% tab title="Liquidity Providers" %}
* [Add Your Favourite Tokens](../../../kyberswap-solutions/kyberswap-interface/user-guides/add-your-favourite-tokens.md)
* [Earn Yield By Contributing Liquidity](../../../kyberswap-solutions/kyberswap-interface/user-guides/earn-yield-by-contributing-liquidity.md)
{% endtab %}
{% endtabs %}
