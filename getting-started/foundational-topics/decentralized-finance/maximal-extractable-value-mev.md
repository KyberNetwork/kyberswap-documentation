---
description: DeFi's Scalpers
---

# Maximal Extractable Value (MEV)

## Overview

Maximal Extractable Value (MEV) are strategies used to realise a risk-free profit from front-running pending network transactions. As transactions are only finalised after being mined in a block, MEV takes advantage of the time premium of publicly available pending transactions in order to reprioritise transactions. As such, MEV extracts value from the system based on how public blockchains prioritize transactions.

## The information premium <a href="#0868" id="0868"></a>

To understand MEV, we first need to go back to how transactions are confirmed on the network. Currently, for the majority of PoW or PoS chains, a user signals their willingness for their transaction to be finalized on the chain by paying a gas fee. This transaction processing fee is required to ensure that the user sends a genuine transaction as they stand to lose this fee if the transaction is malicious. Where this fee gets interesting is due to the fact that each new block on the network has a limited amount of space to which transactions can be added. In other words, the network is only able to process a limited number of transactions and needs a way to prioritise transactions.

Aside from validating new blocks, miners also have the responsibility to propose new blocks and this is where things start to get tricky. In a conventional scenario, a user signals their willingness for faster transaction confirmation times by increasing the gas fee which they are willing to pay. On the other side, miners would select the transaction with the highest gas prices from the transaction queue as this would maximize their profits. Plain and simple as this ensures that the miner is indifferent to the transaction contents and prioritizes based on the fee alone. The complication arises due to the presence of a publicly available transaction queue.

All transactions on such networks will first have to be added to a queue (mempool) in order to be picked up by the miner. This queue is necessarily public given the transparency that public blockchains affords. Where an unsuspecting user might be caught off-guard is when the details of their transaction is used against them prior to being finalized on the network. Remember that it takes time for a transaction to be finalized (ie added to a block) and within this time, this information could be capitalized on as it had already been signed by the user. Of note, this is not only restricted to miners as third-parties who see such information are able to propose transactions with a higher gas fee to get their transaction priotitized.

## The time premium <a href="#7536" id="7536"></a>

The information above is only valuable as long as the transaction has yet to be finalized. As such, the transaction confirmation duration sets an upper bound on the time value of such information, after which the information is essentially worthless to the MEV strategy. Given that ETH block times are approximately [\~12 seconds](https://ycharts.com/indicators/ethereum\_average\_block\_time), this doesn’t give much time for the MEV strategy to be carried out. As such, MEV is usually carried out by bots which generally does the following:

* Monitor the transaction queue for transactions which meet their specific criteria
* Calculate profitability based on available information. This will also have to take into account the gas costs
* If there is a profit to be made, form a transaction based on the calculated parameters
* Send the transaction with a higher gas fee to front-run the targeted transaction
* Monitor the sequence of transaction confirmation as there is still the possibility of the target transaction being confirmed first. If so, cancel the MEV transaction

Efficiency is key here as every second the MEV transaction is delayed means the bot is closer to missing out on being included for that block. The above is taking into account a single bot but realistically, there would be plenty of bots each trying to get a piece of the pie. As such, in addition to having to be as efficient as the competition, network latency also plays a critical role to the success of the strategy.

As most blockchains default to gas fee to prioritize transactions, bots instead compete to be the the first in queue when a block is proposed. Notice that a block proposer has between the confirmation of the last block and the finalisation of the next block to propose a block. As such, the timing of block creation is not fixed and the only thing that the bots can do is outbid other bots in hopes that the block proposer will select their transaction upon finalizing the block template. Bots can submit a transaction with a prohibitively high gas fee but that would mean they significantly diminish their profits. What is more likely is that the bots will incrementally outbid each other by monitoring other bot transactions. This means that lower latency provides a competitive advantage to such strategies.

## Capitalizing on the premiums <a href="#b4f4" id="b4f4"></a>

Given the above background, there are a number of ways where profits can be extracted via reordering, including, or excluding transactions within a block. Do remember that all of the below strategies aim for their MEV transaction to be included in the same block or before the target transaction confirmation.

### Sandwich attack <a href="#1669" id="1669"></a>

A bot monitors the queue for a large incoming trade. Large trades would usually result in slippage which is the difference between the quoted price at the time when the user confirmed the trade and the effective price when the trade was confirmed.

Upon identifying a target trade, say in this case a trader is swapping 100ETH to KNC, the bot will buy up KNC before the target trade is approved. This increases the effective price of KNC which the bot then sells back to the trader. From the trader’s perspective, this increases their slippage and hence their cost price of the equivalent KNC received.

### Arbitrage <a href="#cc44" id="cc44"></a>

A bot monitors the queue for a large incoming trade. Upon identifying the target trade, the bot calculates the implied price movement on the specific exchange where the trade is placed. The bot queries the price across other exchanges (decentralised but also centralised if they have sufficient capital) and compares the price impact above to determine profitability.

Using the same example above, the bot buys KNC from other exchanges and immediately sells it to the exchange where the target trade is taking place. This increases the effective price of KNC for the trader.

### Sniping <a href="#03a2" id="03a2"></a>

There are two forms of sniping which takes place in crypto:

* **AMM liquidity adjustments**: Specific to AMMs, sniping is a specific form of MEV whereby an attacker jumps in front of normal liquidity providers by adding and removing liquidity just before and right after a huge swap.
* **Token releases**: A bot monitors the queue for transactions which are intended to buy newly released tokens/NFTs. As there is usually a rush of users trying to get their hands on the new token, the price of the token tends to increase rapidly upon launch. Based on the purchase transactions submitted by the users, the bot can determine if it is able to obtain the token by front running the user and then selling it to them at a significantly higher price.

### Liquidation <a href="#87e9" id="87e9"></a>

A bot monitors the queue for liquidator transactions. Upon identifying a target transaction, the bot forms a liquidation transaction and sends it to the network with a higher fee. As such, the bot did not actually identify the liquidation event that was triggered but instead capitalised on the liquidators’ slower transaction.

## Miners ++, MEV-Party +, Users -- <a href="#ddd2" id="ddd2"></a>

Of note, the strategies above could be used by both miners or MEV-parties but in either case, the miner still stands to benefit the most from such strategies. This is especially so if the miner is also the MEV-party as block producers do not need to include a transaction fee to incentivize transactions to be included in a block.

The MEV-party stands to pocket the additional slippage in trades or front-running key token events. The miner benefits from the increased gas prices due to MEV bots outbidding each other. All the above comes at the expense of a degraded user experience as trades are always settled at the highest price, fees are consistently high, and any profit opportunities identified are effectively snatched away.&#x20;

## Protocol +/- ? <a href="#c289" id="c289"></a>

While it could be argued that MEV is part of the market efficiency in order to iron out information asymmetries, where the line is blurred is in access to the MEV tooling. Much of the MEV strategies detailed above require a fair bit of know-how in order to be executed. Moreover, the initial capital required might be quite significant to the average person especially when the gas fees are high, which is likely to be the case with all the MEV bots. This means that knowledgeable parties with sufficient capital reap the rewards in terms of MEV but this could potentially come at the cost of protocol security.

As a start, if the degraded user experience outweighs the benefits of using the network, community members might choose to leave the network. For the DeFi space, this has to be taken into account within the context of centralised exchanges which would technically not face such problems. Users might move their trades to centralised exchanges which then reduces decentralisation guarantees.

A more existential question is what happens when the MEV to block rewards ratio starts tilting in favor of MEV. In this scenario, it is more profitable for miners (who themselves are assumed to have a pure profit incentive) to start using MEV strategies instead of securing the network. Of course the MEV strategies wouldn’t exist without the blocks being created. However, taken as a whole, the network will not be able to provide reasonable guarantees that a transaction would be included based purely on the gas fee.

Taking this a step further, miners could even rewrite blockchain history in what is called a [time-bandit attack](https://www.mev.wiki/attack-examples/time-bandit-attack). By re-mining past blocks, all MEV extracted in the previous blocks could be used to subsidise the attack. This makes rational sense the higher the MEV to block reward ratio.\


* The explosion of DeFi meant significantly more value being transacted on-chain. Moreover, the market cap of ERC20 tokens has exploded relative to ETH.
* During the bull run, transaction fees managed to outpace block rewards meaning that more value is being extracted through unconventional means.
* Increased sophistication and adoption of MEV strategies meaning that this is no longer limited to a niche group of traders.

The second point above is what is concerning as it is hard to argue that such unconventional MEV strategies are of more value than securing the network.

## Protecting our LPs

[KyberSwap Elastic](../../../liquidity-solutions/kyberswap-elastic/) comes with an [anti-sniping feature](../../../liquidity-solutions/kyberswap-elastic/concepts/anti-sniping-mechanism.md) to natively protect LPs from any potential front-runners. This lock based vested reward system eliminates any front-running opportunities brought about from liquidity additions or removals. Refer to [Anti-Sniping Mechanism](../../../liquidity-solutions/kyberswap-elastic/concepts/anti-sniping-mechanism.md) for more information on how Elastic keeps its LPs safe.

For traders, the KyberSwap Aggregator allows you to [customize the maximum slippage](broken-reference) for each trade. This minimizes any front-running opportunities linked to your trade as your trade will only be executed if the final price is within the interval set.

{% tabs %}
{% tab title="Liquidity Providers" %}
* [Elastic Pool Creation](../../../liquidity-solutions/kyberswap-elastic/user-guides/elastic-pool-creation.md)
* [Add Liquidity To An Existing Classic Pool](../../../liquidity-solutions/kyberswap-classic/user-guides/add-liquidity-to-an-existing-classic-pool.md)
* [Increasing Liquidity On Elastic](../../../liquidity-solutions/kyberswap-elastic/user-guides/increasing-liquidity-on-elastic.md)
{% endtab %}

{% tab title="Traders" %}
* [Customize trade parameters](broken-reference)
* [Instantly Swap At Superior Rates](broken-reference)
{% endtab %}
{% endtabs %}
