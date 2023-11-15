# Elastic Zap

{% hint style="info" %}
**Introduction To Zaps**

For a conceptual overview of zapping, please refer to our primer on [Zap](../../../getting-started/foundational-topics/decentralized-finance/zap.md).
{% endhint %}

## Concentrated Liquidity Zaps

KyberSwap is bringing an even more convenient LP experience by enabling zaps on KyberSwap Elastic. Unlike zaps on constant product pools where all pool liquidity is fungible (i.e. distributed equally across the whole price curve), zaps on concentrated liquidity pools need to take into account liquidity distribution across customized position ranges (see [Tick-Range Mechanism](tick-range-mechanism.md) for more info). This adds significantly more complexity when implementing zaps on CLMM-type pools such as KyberSwap Elastic.

To enable LPs the option to zap into Elastic, KyberSwap has codified all the above complexities into zap-specific contracts which extends upon the core functionalities of the Elastic pool contracts. By functionally separating core and convenience operations, this paves the way for even more innovation based on contract modularity. The full list of Elastic Zap contract addresses can be found [here](../contracts/elastic-zap-contract-addresses.md).

## Minimizing Price Impact & Impermanent Loss

Aside from a much simpler LP experience, Elastic Zap is also primed to maximize LP yields through its integration with the [KyberSwap Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/). By taking the additional step of scanning for more optimal rates across [multiple DEXs](../../../getting-started/supported-exchanges-and-networks.md), Elastic Zap greatly reduces LPs exposure to price impact and the resulting IL risks.

{% hint style="info" %}
**A Note On Gas Costs**

Due to the complexity and multitude of steps required to achieve CLMM zaps with aggregator integration, zap transactions tend to consume more gas.

Nonetheless this has to be baselined against multiple swap + add transactions if the liquidity addition were to happen manually. In most cases when adding liquidity with a single token, this entails:

* Initial swap from `tokenA` -> `tokenB` (requires manually calculating token ratio requirement)
* Based on token ratio requirements, add the lower of `tokenA`:`tokenB` amounts
* If the pool price moved between swap and add liquidity, repeat the process above for the remaining amount of `tokenA` or `tokenB`

For more active pools (or those with lower fee tiers), the pool price is more likely to move between the initial swap and liquidity addition. Critically, the narrower the position range selected and the closer the range boundaries are to the pool price, the larger the shift in token ratios required if the pool price changes.

Furthermore, the market for actively traded pairs will make sourcing the exact amounts from a market order extremely difficult. This is compounded for large trades where price impact considerations come into play.

Consequently, LPs would usually have to swap + add liquidity multiple times before their initial capital value has been fully added to CLMM pools. As DeFi users ourselves, we are also wary of this gas costs and are constantly exploring new ways to optimize gas usage. Expect cheaper Elastic Zaps as we continue to iterate upon our code base across multiple chains.
{% endhint %}

### Aggregator Integration

When sourcing the token ratio for a zap in, swaps can be executed via the target pool itself or via other liquidity sources. In the latter case, LPs do not have to worry about the target pool price changing as a result of the swap transaction. That is, the pool which the LP is adding liquidity to will not experience a state change as the swap occurs external to the pool.&#x20;

As a consequence of the [AMM](../../../getting-started/foundational-topics/decentralized-finance/automated-market-maker.md) design, swapping against the pool prior to liquidity addition introduces additional technical complexities when computing the token ratio to be added (because the swap will change the pool price before addition). Critically, while the above can be solved mathematically, such LPs could also be exposed to further IL risks as a result of the zap in direction. This is especially so in cases where the pool price varies significantly from the market price.

The example below highlights this fact conceptually when swapping against the target pool:

* Target pool price is 1WETH:2,000USDC
* LP zaps in 1,000USDC to the USDC-WETH pool
* Assuming an equal ratio of tokens required, the token add liquidity ratio is 500USD worth of WETH and 500USD worth of USDC -> 0.25WETH:500USDC
* Contract swaps the LP's 500USDC -> 0.25WETH against the target pool
* The LP's 500USDC is added to the pool and 0.25WETH is transferred from the pool to the LP
* As the pool now has more USDC relative to WETH, the pool price is now higher than the initial 1WETH:2,000USDC (i.e. WETH has gotten more expensive relative to USDC from the perspective of the pool)
* Liquidity is added at the new pool price above the initial 1WETH:2,000USDC

In short, **the** [**price impact**](../../../getting-started/foundational-topics/decentralized-finance/price-impact.md) **of the intermediate swap will result in the newly created zap position being added further away from the market price** (assuming pool price before swap = market price). Depending on the market direction, this might result in immediate IL upon creation of the position. This is compounded in cases where the target pool TVL is low relative to the trade volume.

To minimize such risks, [KyberSwap Elastic Zap](elastic-zap.md) leverages the [KyberSwap Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/) to ensure that LPs always get superior rates when sourcing the intermediate swap. The Aggregator will compare rates across [all integrated DEX liquidity sources](../../../getting-started/supported-exchanges-and-networks.md) against the resulting target pool price (if intermediate swap was against the pool) and optimize the zap route accordingly. This minimizes the potential IL risks that LPs face when zapping into Elastic pools.
