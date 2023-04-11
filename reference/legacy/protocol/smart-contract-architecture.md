# Smart Contract Architecture

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

### Kyber Core Smart Contract Overview[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#kyber-core-smart-contract-overview) <a href="#kyber-core-smart-contract-overview" id="kyber-core-smart-contract-overview"></a>

The three main components of any implementation of the Kyber protocol are the Kyber Core Smart Contracts, the Reserve Interface and the List of Registered Reserves and Token Pairs.

![Smart Contract Overview](https://docs.kyberswap.com/assets/images/smartcontractoverview-6cbdd139e306f5e4ce94ac9c62d3d1e9.png)

In our implementation of the protocol, these 3 components are represented by the `KyberNetwork.sol` and `IKyberReserve.sol` contracts. The `KyberNetworkProxy.sol` contract will act as a single endpoint for makers and takers to interface with in order to interact with our liquidity network. The contract will also contain a list of registered reserves that will be iterated through when processing a trade.

With upgradeability in mind, we have designed some auxiliary contracts, such as `KyberMatchingEngine.sol`, `KyberFeeHandler.sol` and `KyberStorage.sol`, will be deployed to help the main `KyberNetwork.sol` contract achieve the core functionalities of the protocol.

### Reserves Overview[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#reserves-overview) <a href="#reserves-overview" id="reserves-overview"></a>

The `IKyberReserve.sol` is the interface that all reserve implementations are required to adhere to.

![Kyber Reserve Interface Overview](https://docs.kyberswap.com/assets/images/kyberreserveinterfaceoverview-ddb6637beed39051f21335a81a8b51fa.png)

Our existing codebase contains 3 types of reserves; Fed Price Reserve, Automated Price Reserve and the Orderbook Reserve. The functions of these reserves are encapsulated within the `KyberReserve.sol` contract. While each reserve type was designed with different features in mind, they share a common goal of contributing liquidity to the network.

#### Fed Price Reserve[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#fed-price-reserve) <a href="#fed-price-reserve" id="fed-price-reserve"></a>

![Fed Price Reserve](https://docs.kyberswap.com/assets/images/fedpricereserve-dd3af8f5468951ad76891eca6cd5d957.png)

The Fed Price Reserve (FPR) is our first type of reserve, offering reserve managers full control and flexibility over their pricing algorithm. However, the flexibility of managing a Fed Price Reserve came with a relatively steep learning curve and development costs that arose from having to build, run, and maintain an off-chain server and/or scripts to feed prices on-chain.

The FPR and conversion rates are represented by the `KyberReserve.sol` and `ConversionRates.sol` contracts respectively. The token conversion rates are fed to the `ConversionRates.sol` contract by the reserve managers. Furthermore, they also have the option of defining the upper and lower limits on the conversion rates via the `SanityRates.sol` contract.

#### Automated Price Reserve[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#automated-price-reserve) <a href="#automated-price-reserve" id="automated-price-reserve"></a>

![Automated Price Reserve](https://docs.kyberswap.com/assets/images/automatedpricereserve-fa74197c258bb46ce5de9941e48d5d5b.png)

The Automated Price Reserve (APR) is the second type of reserve, which was designed with ease of maintenance as the top consideration. Unlike the Fed Price Reserve (FPR), reserve managers of the APR will delegate the control of their pricing strategy to a predefined algorithm set in the smart contract. But in exchange, they will no longer incur the development costs that arose from having to build, run, and maintain an off-chain server and/or scripts to feed prices on-chain.

#### Orderbook Reserve[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#orderbook-reserve) <a href="#orderbook-reserve" id="orderbook-reserve"></a>

The Orderbook Reserve will be updated to be compatible with the Katalyst upgrade.

### Maintainer Overview[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#maintainer-overview) <a href="#maintainer-overview" id="maintainer-overview"></a>

![Maintainer Overview](https://docs.kyberswap.com/assets/images/maintaineroverview-e8d76d8d5e5e888c47ae3a0d5ddbd291.png)

Maintainers are entities within the ecosystem that have access to the functions for adding and removing reserves and token pairs. Currently, the maintainers are Kyber's team members.

### Exchange Overview[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#exchange-overview) <a href="#exchange-overview" id="exchange-overview"></a>

The liquidity network allows takers to convert one type of token (e.g. KNC) and receive a different token in return (e.g. DAI) according to the best rates provided by the reserves. The entire process happens in a single atomic transaction, so we can be assured that there is no partial execution of a trade. A conversion between KNC to DAI is depicted in the diagram below:

![KNC to DAI](https://docs.kyberswap.com/assets/images/tradeSequence-2f8a88f79dc633c9aaa54f7711d2ceab.png)

* A taker (e.g. end user wallets, smart contracts, trading bots) initiates the trade function from `KyberNetworkProxy.sol`.
* `KyberNetworkProxy.sol` forwards the trade request to `KyberNetwork.sol`.
* `KyberNetwork.sol` calls `KyberMatchingEngine.sol` to fetch the list of reserves supporting the KNC-ETH and ETH-DAI trade.
* `KyberMatchingEngine.sol` calls `KyberStorage.sol` to fetch the full reserves list.
* `KyberMatchingEngine.sol` applies the user-specified reserve route(s) for the trades, and returns the final reserve list to `KyberNetwork.sol`.
* `KyberNetwork.sol` queries the rates from each reserves specified in the list. If necessary, a call is made to `KyberMatchingEngine` to determine the best rate(s) for the trade, whilst calculating the trade amounts, network and platform fees required for the trade.
* `KyberNetwork.sol` executes the trades with the reserve(s), who will send the DAI tokens to the taker.
* If there are excess KNC tokens, `KyberNetwork.sol` will send them to the taker.
* Finally, `KyberNetwork.sol` sends the network and platform fees (calculated and collected in ETH) to `KyberFeeHandler`.

### Stack[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#stack) <a href="#stack" id="stack"></a>

Starting from the client and ending in the Ethereum blockchain, we can visualize the entire stack as seen in the figure below:

![Stack](https://docs.kyberswap.com/assets/images/stack-373bf4809ba33e16c2bc1b7fa2f0adf5.png)

### Permissions[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#permissions) <a href="#permissions" id="permissions"></a>

Every contract in the Kyber protocol has three permission groups:

#### 1. Admin[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#1-admin) <a href="#1-admin" id="1-admin"></a>

The admin account is unique (usually cold wallet) and handles infrequent, manual operations like listing new tokens in the exchange. All sensitive operations (e.g. fund related) are limited to the admin address.

#### 2. Operators[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#2-operators) <a href="#2-operators" id="2-operators"></a>

The operator account is a hot wallet and is used for frequent updates like setting reserve rates and withdrawing funds from the reserve to addresses that have been whitelisted by the admin address.

#### 3. Alerters[​](https://docs.kyberswap.com/Legacy/smart-contract-architecture#3-alerters) <a href="#3-alerters" id="3-alerters"></a>

The alerter account is also a hot wallet and is used halt the execution due to inconsistencies in the system (e.g., strange conversion rates). In such cases, the reserve operation is suspended and can be resumed only by the admin address.
