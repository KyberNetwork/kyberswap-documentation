# Overview

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

![Protocol Overview](https://docs.kyberswap.com/assets/images/protocoloverview-0ec8b361405064c8b7af57520fe42aac.png)

The protocol implementation consists of a set of network contract(s), a reserve interface and a list of registered reserves and token pairs. The network diagram above shows an overview of the various actors that interacts with the protocol implementation.

### Network Actors[​](https://docs.kyberswap.com/Legacy/protocol-overview#network-actors) <a href="#network-actors" id="network-actors"></a>

#### Kyber Core Smart Contracts[​](https://docs.kyberswap.com/Legacy/protocol-overview#kyber-core-smart-contracts) <a href="#kyber-core-smart-contracts" id="kyber-core-smart-contracts"></a>

The Kyber Core Smart Contracts contains the implementation of the major protocol functions to allow actors to join and interact with the network. The method signatures of these functions can be seen in the next diagram.

![Kyber Core Smart Contracts](https://docs.kyberswap.com/assets/images/kybercoresmartcontracts-96d644d33953c817fe1b64d16d3989a6.png)

#### Takers[​](https://docs.kyberswap.com/Legacy/protocol-overview#takers) <a href="#takers" id="takers"></a>

A taker is an entity that takes the liquidity provided by the registered reserves by calling the `tradeWithHintAndFee()` function in the Kyber Core Smart Contracts to trade from one token to another token. A taker can be any blockchain entity including end user address, decentralized exchanges, or any smart contracts.

#### Reserves[​](https://docs.kyberswap.com/Legacy/protocol-overview#reserves) <a href="#reserves" id="reserves"></a>

Reserves are liquidity providers in the network that contributes liquidity in terms of tokens inventory and prices on their smart contracts.

**Reserve Interface**[**​**](https://docs.kyberswap.com/Legacy/protocol-overview#reserve-interface)

<figure><img src="https://docs.kyberswap.com/assets/images/reserveinterface-506494754a05ec844b03c92900f63552.png" alt=""><figcaption></figcaption></figure>

&#x20;The reserve interface defines the contract functions which reserves are required to conform to. Note that the reserve interface above is a general template of what the reserve interface should look like. The interface may be tweaked further to better suit the needs of the respective blockchains.

Only by complying with the interface will network maintainers be able to register a reserve to the Kyber Core Smart Contracts. The exact implementation details of how reserves determine prices and manage its inventory is not explicitly defined in the protocol and is at the discretion of the developers of these reserves.

**Registered Reserve**[**​**](https://docs.kyberswap.com/Legacy/protocol-overview#registered-reserve)

A list of reserves that will be iterated through when rates are queried or to facilitate a trade.

#### Maintainers[​](https://docs.kyberswap.com/Legacy/protocol-overview#maintainers) <a href="#maintainers" id="maintainers"></a>

Maintainers refer to anyone who has permissions to access the functions for the adding/removing of reserves and token pairs, such as a DAO or the team behind the protocol implementation.
