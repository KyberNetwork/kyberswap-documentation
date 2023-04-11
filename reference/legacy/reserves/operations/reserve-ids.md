# Reserve IDs

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

### What are reserve IDs?[​](https://docs.kyberswap.com/Legacy/reserves/operation/reserve-ids#what-are-reserve-ids) <a href="#what-are-reserve-ids" id="what-are-reserve-ids"></a>

Instead of Ethereum addresses, reserves are now identified using reserve IDs. Each reserve ID is 32 bytes long.\
_Example: 0xaa4b4e4320415052000000000000000000000000000000000000000000000000_

### Why are reserve IDs used instead of addresses?[​](https://docs.kyberswap.com/Legacy/reserves/operation/reserve-ids#why-are-reserve-ids-used-instead-of-addresses) <a href="#why-are-reserve-ids-used-instead-of-addresses" id="why-are-reserve-ids-used-instead-of-addresses"></a>

Reserve addresses can change in the event of reserve upgrades or reserve migrations. As an example, if Uniswap does an upgrade, then the Uniswap Bridge Reserve must be upgraded as well, and thus, a new address for the Uniswap Bridge Reserve is used.

With the new Reserve Routing feature for takers, and as reserves may upgrade their contracts over time (and thus have changing reserve addresses), we utilise reserve IDs for a more stable identity.
