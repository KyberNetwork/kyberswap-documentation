# Platform Fees

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

### Introduction[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#introduction) <a href="#introduction" id="introduction"></a>

Ethereum allows smart contracts to emit events during the execution of a function. Your application can track these events to find information such as trades, platform fees, reserve rebates, KNC burnt etc.

Using these events, you will be able to calculate other important information such as overall volume, volume per token, volume per reserve, and more. Our [in-house built tracker](https://tracker.kyber.network/) uses the events emitted to track these statistics.

### Volume and Trade Events[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#volume-and-trade-events) <a href="#volume-and-trade-events" id="volume-and-trade-events"></a>

The `ExecuteTrade` event is emitted by the KyberNetworkProxy contracts.

* [ExecuteTrade V2](https://docs.kyberswap.com/Legacy/integrations/platform-fees#executetrade-v2)
* [ExecuteTrade V1](https://docs.kyberswap.com/Legacy/integrations/platform-fees#executetrade-v1)

The `KyberTrade` event is emitted by the KyberNetwork contracts.

* [KyberTrade V2](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kybertrade-v2)

### Fee Tracking Events[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#fee-tracking-events) <a href="#fee-tracking-events" id="fee-tracking-events"></a>

The following events are emitted by the KyberFeeHandler contract(s).

* [FeeDistributed](https://docs.kyberswap.com/Legacy/integrations/platform-fees#feedistributed)
* [BRRUpdated](https://docs.kyberswap.com/Legacy/integrations/platform-fees#brrupdated)
* [KncBurned](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kncburned)
* [RewardsRemovedToBurn](https://docs.kyberswap.com/Legacy/integrations/platform-fees#rewardsremovedtoburn)

### Events to track Fed Price Reserve (FPR) and Automated Price Reserve (APR) statistics[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#events-to-track-fed-price-reserve-fpr-and-automated-price-reserve-apr-statistics) <a href="#events-to-track-fed-price-reserve-fpr-and-automated-price-reserve-apr-statistics" id="events-to-track-fed-price-reserve-fpr-and-automated-price-reserve-apr-statistics"></a>

These events are emitted by the FPRs and APRs.

* [TradeExecute](https://docs.kyberswap.com/Legacy/integrations/integrations-contractevents.md#tradeexecute)
* [DepositToken](https://docs.kyberswap.com/Legacy/integrations/integrations-contractevents.md#deposittoken)
* [WithdrawFunds](https://docs.kyberswap.com/Legacy/integrations/integrations-contractevents.md#withdrawfunds)

### Historical Events[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#historical-events) <a href="#historical-events" id="historical-events"></a>

These events are no longer emitted, but remain documented.

* [KyberTrade V1](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kybertrade-v1)
* [AssignBurnFees](https://docs.kyberswap.com/Legacy/integrations/platform-fees#assignburnfees)
* [AssignFeeToWallet](https://docs.kyberswap.com/Legacy/integrations/platform-fees#assignfeetowallet)
* [BurnAssignedFees](https://docs.kyberswap.com/Legacy/integrations/platform-fees#burnassignedfees)
* [SendWalletFees](https://docs.kyberswap.com/Legacy/integrations/platform-fees#sendwalletfees)

### [KyberNetworkProxy](https://docs.kyberswap.com/Legacy/integrations/addresses-mainnet.md#kybernetworkproxy)[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kybernetworkproxy) <a href="#kybernetworkproxy" id="kybernetworkproxy"></a>

_Contract Address_: [0x9AAb3f75489902f3a48495025729a0AF77d4b11e](https://etherscan.io/address/0x9AAb3f75489902f3a48495025729a0AF77d4b11e)\
_Source_: [KyberNetworkProxy.sol](https://github.com/KyberNetwork/smart-contracts/blob/Katalyst/contracts/sol6/KyberNetworkProxy.sol)

#### `ExecuteTrade (V2)`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#executetrade-v2) <a href="#executetrade-v2" id="executetrade-v2"></a>

Event is emitted when a trade is executed.

event **ExecuteTrade**(address indexed trader, IERC20 src, IERC20 dest, address destAddress, uint256 actualSrcAmount, uint256 actualDestAmount, address platformWallet, uint256 platformFeeBps)

| Parameter         | Type             | Indexed | Description                                        |
| ----------------- | ---------------- | ------- | -------------------------------------------------- |
| `trader`          | address          | YES     | trader's address                                   |
| `src`             | IERC20           | NO      | source ERC20 token contract address                |
| `dest`            | IERC20           | NO      | destination ERC20 token contract address           |
| `destAddress`     | address          | NO      | destination address for receiving `dest` tokens    |
| `actualSrcAmount` | uint256          | NO      | `src` token wei amount                             |
| `platformWallet`  | address          | NO      | wallet address receiving trade fees                |
| `platformFeeBps`  | `platformFeeBps` | NO      | platform fee percentage (in basis points) of trade |

Event Signature: `0xf724b4df6617473612b53d7f88ecc6ea983074b30960a049fcd0657ffe808083`

### [KyberNetworkProxy (V1)](https://docs.kyberswap.com/Legacy/integrations/addresses-mainnet.md#kybernetworkproxy-v1)[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kybernetworkproxy-v1) <a href="#kybernetworkproxy-v1" id="kybernetworkproxy-v1"></a>

_Contract Address_: [0x818E6FECD516Ecc3849DAf6845e3EC868087B755](https://etherscan.io/address/0x818E6FECD516Ecc3849DAf6845e3EC868087B755)\
_Source_: [KyberNetworkProxy.sol](https://github.com/KyberNetwork/smart-contracts/blob/master/contracts/KyberNetworkProxy.sol)

#### `ExecuteTrade (V1)`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#executetrade-v1) <a href="#executetrade-v1" id="executetrade-v1"></a>

Event is emitted when a trade is executed.

event **ExecuteTrade**(address indexed sender, ERC20 src, ERC20 dest, uint actualSrcAmount, uint actualDestAmount)

| Parameter          | Type    | Indexed | Description                              |
| ------------------ | ------- | ------- | ---------------------------------------- |
| `sender`           | address | YES     | sender's address                         |
| `src`              | ERC20   | NO      | source ERC20 token contract address      |
| `dest`             | ERC20   | NO      | destination ERC20 Token contract address |
| `actualSrcAmount`  | uint    | NO      | source ERC20 token amount in wei         |
| `actualDestAmount` | uint    | NO      | destination ERC20 token amount in wei    |

Event Signature: `0x1849bd6a030a1bca28b83437fd3de96f3d27a5d172fa7e9c78e7b61468928a39`

### [KyberNetwork](https://docs.kyberswap.com/Legacy/integrations/addresses-mainnet.md#kybernetwork)[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kybernetwork) <a href="#kybernetwork" id="kybernetwork"></a>

_Contract Address_: [0x7C66550C9c730B6fdd4C03bc2e73c5462c5F7ACC](https://etherscan.io/address/0x7C66550C9c730B6fdd4C03bc2e73c5462c5F7ACC)\
_Source_: [KyberNetwork.sol](https://github.com/KyberNetwork/smart-contracts/blob/Katalyst/contracts/sol6/KyberNetwork.sol)

#### `KyberTrade (V2)`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kybertrade-v2) <a href="#kybertrade-v2" id="kybertrade-v2"></a>

Emitted when a trade is executed in the internal network.

event **KyberTrade**(IERC20 indexed src, ERC20 indexed dest, uint256 ethWeiValue, uint256 networkFeeWei, uint256 customPlatformFeeWei, bytes32\[] t2eIds, bytes32\[] e2tIds, uint256\[] t2eSrcAmounts, uint256\[] e2tSrcAmounts, uint256\[] t2eRates, uint256\[] e2tRates)

|        Parameter       |    Type    | Indexed |                       Description                      |
| :--------------------: | :--------: | :-----: | :----------------------------------------------------: |
|          `src`         |    ERC20   |   YES   |           source ERC20 token contract address          |
|         `dest`         |    ERC20   |   YES   |        destination ERC20 token contract address        |
|      `ethWeiValue`     |   uint256  |    NO   |              ether wei value of the trade              |
|     `networkFeeWei`    |   uint256  |    NO   |                network fee in ether wei                |
| `customPlatformFeeWei` |   uint256  |    NO   |                platform fee in ether wei               |
|        `t2eIds`        | bytes32\[] |    NO   |      token -> ether reserve IDs used for the trade     |
|        `e2tIds`        | bytes32\[] |    NO   |      Ether to token reserve IDs used for the trade     |
|     `t2eSrcAmounts`    | uint256\[] |    NO   |    token -> ether source amounts in source token wei   |
|     `e2tSrcAmounts`    | uint256\[] |    NO   | Ether to token source amounts in destination token wei |
|       `t2eRates`       | uint256\[] |    NO   |         token -> ether rates used for the trade        |
|       `e2tRates`       | uint256\[] |    NO   |         Ether to token rates used for the trade        |

Event Signature: `0xc6efb0df0b5d684cd6482e00270d068229ca5833634798e25f85b79eee5183f9`

**Note**[**​**](https://docs.kyberswap.com/Legacy/integrations/platform-fees#note)

* For token to token trades, the `ethWeiValue` will be just 1 side of the trade. As an example, X KNC -> 10 ETH -> Y DAI yields `ethWeiValue = 10e18`.

### [KyberFeeHandler (ETH)](https://docs.kyberswap.com/Legacy/integrations/addresses-mainnet.md#kyberfeehandler-eth)[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kyberfeehandler-eth) <a href="#kyberfeehandler-eth" id="kyberfeehandler-eth"></a>

_Contract Address_: [0xd3d2b5643e506c6d9B7099E9116D7aAa941114fe](https://etherscan.io/address/0xd3d2b5643e506c6d9B7099E9116D7aAa941114fe)\
_Source_: [KyberFeeHandler.sol](https://github.com/KyberNetwork/smart-contracts/blob/Katalyst/contracts/sol6/Dao/KyberFeeHandler.sol)

#### `FeeDistributed`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#feedistributed) <a href="#feedistributed" id="feedistributed"></a>

Emitted when there are fees to be given to various parties, based on the BRR distribution determined by the KyberDAO.

event **FeeDistributed**(IERC20 indexed token, address indexed platformWallet, uint256 platformFeeWei, uint256 rewardWei, uint256 rebateWei, address\[] rebateWallets, uint256\[] rebatePercentBpsPerWallet, uint256 burnAmtWei)

|          Parameter          |    Type    | Indexed |                       Description                       |
| :-------------------------: | :--------: | :-----: | :-----------------------------------------------------: |
|           `token`           |   IERC20   |   YES   |       token for which fees will be distributed in       |
|       `platformWallet`      |   address  |   YES   |       Wallet address that gets fees from the trade      |
|       `platformFeeWei`      |   uint256  |    NO   |               Platform fee in `token` wei               |
|         `rewardWei`         |   uint256  |    NO   |           KNC stakers' rewards in `token` wei           |
|         `rebateWei`         |   uint256  |    NO   |              Reserve rebates in `token` wei             |
|       `rebateWallets`       | address\[] |    NO   |    List of rebate wallet addresses receiving rebates    |
| `rebatePercentBpsPerWallet` | uint256\[] |    NO   |     Corresponding rebate proportions in basis points    |
|         `burnAmtWei`        |   uint256  |    NO   | `token` wei allocated for converting to and burning KNC |

Event Signature: `0xd66a6cfa04148d5e34fd3da6bbabc8a7e6c9ebffb1638f00e9c35d67b51c6bd2`

#### `BRRUpdated`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#brrupdated) <a href="#brrupdated" id="brrupdated"></a>

Emitted when there is a change made to the BRR distribution, as determined by the KyberDA

event **BRRUpdated**(uint256 rewardBps, uint256 rebateBps, uint256 burnBps, uint256 expiryTimestamp, uint256 indexed epoch)

|     Parameter     |   Type  | Indexed |                                Description                               |
| :---------------: | :-----: | :-----: | :----------------------------------------------------------------------: |
|    `rewardBps`    | uint256 |    NO   |  proportion (in basis points) of network fee allocated to staker rewards |
|    `rebateBps`    | uint256 |    NO   | proportion (in basis points) of network fee allocated to reserve rebates |
|     `burnBps`     | uint256 |    NO   |   proportion (in basis points) of network fee allocated to burning KNC   |
| `expiryTimestamp` | uint256 |    NO   |       timestamp after which this BRR configuration will be invalid       |
|      `epoch`      | uint256 |   YES   |                           current epoch number                           |

Event Signature: `0x90da252e8e1873b40c0a15bba09620de70b1550bcd36e796175beb6f259c797d`

#### `KNCBurned`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kncburned) <a href="#kncburned" id="kncburned"></a>

Emitted when KNC has been burnt.

event **KncBurned**(uint256 kncTWei, IERC20 indexed token, uint256 amount)

| Parameter |   Type  | Indexed |                       Description                      |
| :-------: | :-----: | :-----: | :----------------------------------------------------: |
| `kncTWei` | uint256 |    NO   |            KNC burnt amont in KNC token wei            |
|  `token`  |  IERC20 |   YES   |         token for which KNC was converted from         |
|  `amount` | uint256 |    NO   | `token` wei amount used for conversion and burning KNC |

Event Signature: `0xd66a6cfa04148d5e34fd3da6bbabc8a7e6c9ebffb1638f00e9c35d67b51c6bd2`

#### `RewardsRemovedToBurn`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#rewardsremovedtoburn) <a href="#rewardsremovedtoburn" id="rewardsremovedtoburn"></a>

Emitted when an entire epoch's reward has been allocated for burning KNC (Eg. epoch 0).

event **RewardsRemovedToBurn**(uint256 indexed epoch, uint256 rewardsWei)

|   Parameter  |   Type  | Indexed |                         Description                         |
| :----------: | :-----: | :-----: | :---------------------------------------------------------: |
|    `epoch`   | uint256 |   YES   | epoch number for which rewards are entirely for burning KNC |
| `rewardsWei` | uint256 |    NO   |          ether wei amount allocated for burning KNC         |

Event Signature: `0x11c852d8be537f120b8d4b4d5c3c211870522fd96a8bd9fa51d102774077a51b`

### [KyberReserve](https://docs.kyberswap.com/Legacy/integrations/addresses-mainnet.md#kyberreserve)[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kyberreserve) <a href="#kyberreserve" id="kyberreserve"></a>

_Contract Address_: [0x63825c174ab367968EC60f061753D3bbD36A0D8F](https://etherscan.io/address/0x63825c174ab367968EC60f061753D3bbD36A0D8F/)\
_Other Reserves_: Visit our [tracker](https://tracker.kyber.network/#/reserves) to see other reserve addresses.\
_Source_: [KyberReserve.sol](https://github.com/KyberNetwork/smart-contracts/blob/master/contracts/KyberReserve.sol)

#### `DepositToken`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#deposittoken) <a href="#deposittoken" id="deposittoken"></a>

Event is emitted when the contract receives the token deposit.

event **DepositToken**(ERC20 token, uint amount)&#x20;

| Parameter | Type  | Indexed | Description                  |
| --------- | ----- | ------- | ---------------------------- |
| `token`   | ERC20 | NO      | ERC20 token contract address |
| `amount`  | uint  | NO      | ERC20 token amount in wei    |

Event Signature: `0x2d0c0a8842b9944ece1495eb61121621b5e36bd6af3bba0318c695f525aef79f`

#### `TradeEnabled`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#tradeenabled) <a href="#tradeenabled" id="tradeenabled"></a>

Event is emitted when trading is enabled for the reserve.

event **TradeEnabled**(bool enable)&#x20;

| Parameter | Type | Indexed | Description                                                 |
| --------- | ---- | ------- | ----------------------------------------------------------- |
| `enable`  | bool | NO      | `true` if reserve is enabled, otherwise `false` if disabled |

Event Signature: `0x7d7f00509dd73ac4449f698ae75ccc797895eff5fa9d446d3df387598a26e735`

#### `TradeExecute`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#tradeexecute) <a href="#tradeexecute" id="tradeexecute"></a>

Event is emitted when the reserve has executed a trade.

event **TradeExecute**(address indexed origin, address src, uint srcAmount, address destToken, uint destAmount, address destAddress)&#x20;

| Parameter     | Type     | Indexed | Description                                    |
| ------------- | -------- | ------- | ---------------------------------------------- |
| `origin`      | address  | YES     | sender's address                               |
| `src`         | address  | NO      | source ERC20 token contract address            |
| `srcAmount`   | uint     | NO      | wei amount of source ERC20 tokens              |
| `destToken`   | address  | NO      | destination ERC20 token contract address       |
| `destAmount`  | uint     | NO      | wei amount of destination ERC20 tokens         |
| `destAddress` | address  | NO      | recipient address for destination ERC20 tokens |

Event Signature: `0xea9415385bae08fe9f6dc457b02577166790cde83bb18cc340aac6cb81b824de`

#### `WithdrawFunds`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#withdrawfunds) <a href="#withdrawfunds" id="withdrawfunds"></a>

Event is emitted with funds are withdrawn from the reserve.

event **WithdrawFunds**(ERC20 token, uint amount, address destination)&#x20;

| Parameter     | Type    | Indexed | Description                             |
| ------------- | ------- | ------- | --------------------------------------- |
| `token`       | ERC20   | NO      | ERC20 token contract address            |
| `amount`      | uint    | NO      | wei amount of tokens that was withdrawn |
| `destination` | address | NO      | recipient address of withdrawn funds    |

Event Signature: `0xb67719fc33c1f17d31bf3a698690d62066b1e0bae28fcd3c56cf2c015c2863d6`

### KyberNetwork (Old)[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kybernetwork-old) <a href="#kybernetwork-old" id="kybernetwork-old"></a>

_Past Contract Addresses_:\
[v4 - 0x65bF64Ff5f51272f729BDcD7AcFB00677ced86Cd](https://etherscan.io/address/0x65bF64Ff5f51272f729BDcD7AcFB00677ced86Cd/)\
[v3 - 0x9ae49C0d7F8F9EF4B864e004FE86Ac8294E20950](https://etherscan.io/address/0x9ae49C0d7F8F9EF4B864e004FE86Ac8294E20950/)\
[v2 - 0x91a502C678605fbCe581eae053319747482276b9](https://etherscan.io/address/0x91a502c678605fbce581eae053319747482276b9/)\
[v1 - 0x964F35fAe36d75B1e72770e244F6595B68508CF5](https://etherscan.io/address/0x964f35fae36d75b1e72770e244f6595b68508cf5/)

#### `KyberTrade (V1)`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#kybertrade-v1) <a href="#kybertrade-v1" id="kybertrade-v1"></a>

Emitted when a trade is executed in the internal network.

event **KyberTrade**(address indexed trader, ERC20 src, ERC20 dest, uint srcAmount, uint dstAmount, address destAddress, uint ethWeiValue, address reserve1, address reserve2, bytes hint)&#x20;

| Parameter     | Type    | Indexed | Description                                                 |
| ------------- | ------- | ------- | ----------------------------------------------------------- |
| `trader`      | address | YES     | trader's address                                            |
| `src`         | ERC20   | NO      | source ERC20 token contract address                         |
| `dest`        | ERC20   | NO      | destination ERC20 token contract address                    |
| `srcAmount`   | uint    | NO      | source ERC20 token amount                                   |
| `dstAmount`   | uint    | NO      | destination ERC20 token amount                              |
| `destAddress` | ERC20   | NO      | recipient address for destination ERC20 token               |
| `ethWeiValue` | uint    | NO      | Ether wei value of the trade                                |
| `reserve1`    | address | NO      | address of reserve selected for source token -> ether trade |
| `reserve2`    | address | NO      | address of reserve selected for source ether -> token trade |
| `hint`        | bytes   | NO      | used to determine if permissionless reserves are to be used |

Event Signature: `0xd30ca399cb43507ecec6a629a35cf45eb98cda550c27696dcb0d8c4a3873ce6c`

### FeeBurner[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#feeburner) <a href="#feeburner" id="feeburner"></a>

_Past Contract Addresses_:\
[v4 - 0x8007aa43792A392b221DC091bdb2191E5fF626d1](https://etherscan.io/address/0x8007aa43792A392b221DC091bdb2191E5fF626d1/)\
[v3 - 0x52166528FCC12681aF996e409Ee3a421a4e128A3](https://etherscan.io/address/0x52166528FCC12681aF996e409Ee3a421a4e128A3/)\
[v2 - 0xed4f53268bfdFF39B36E8786247bA3A02Cf34B04](https://etherscan.io/address/0xed4f53268bfdFF39B36E8786247bA3A02Cf34B04/)\
[v1 - 0x07f6e905f2a1559cd9fd43cb92f8a1062a3ca706](https://etherscan.io/address/0x07f6e905f2a1559cd9fd43cb92f8a1062a3ca706/)

#### `AssignBurnFees`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#assignburnfees) <a href="#assignburnfees" id="assignburnfees"></a>

Event is emitted when fees for burning are assigned for a reserve.

event **AssignBurnFees**(address reserve, uint burnFee)

| Parameter | Type    | Indexed | Description                        |
| --------- | ------- | ------- | ---------------------------------- |
| `reserve` | address | NO      | reserve's contract address         |
| `burnFee` | uint    | NO      | amount of fees to be burned in wei |

Event Signature: `0xf838f6ddc89706878e3c3e698e9b5cbfbf2c0e3d3dcd0bd2e00f1ccf313e0185`

#### `AssignFeeToWallet`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#assignfeetowallet) <a href="#assignfeetowallet" id="assignfeetowallet"></a>

Event is emitted when fees for fee sharing are assigned for a reserve.

event **AssignFeeToWallet**(address reserve, address wallet, uint walletFee)&#x20;

| Parameter   | Type    | Indexed | Description                                     |
| ----------- | ------- | ------- | ----------------------------------------------- |
| `reserve`   | address | NO      | reserve's contract address                      |
| `wallet`    | address | NO      | wallet address to send fees to                  |
| `walletFee` | uint    | NO      | amount of fees to be assigned to wallet address |

Event Signature: `0x366bc34352215bf0bd3b527cfd6718605e1f5938777e42bcd8ed92f578368f52`

#### `BurnAssignedFees`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#burnassignedfees) <a href="#burnassignedfees" id="burnassignedfees"></a>

Event is emitted when fees are burned.

event **BurnAssignedFees**(address indexed reserve, address sender, uint quantity)

| Parameter  | Type    | Indexed | Description                          |
| ---------- | ------- | ------- | ------------------------------------ |
| `reserve`  | address | YES     | reserve's contract address           |
| `sender`   | address | NO      | sender's address                     |
| `quantity` | uint    | NO      | amount of assigned fees to be burned |

Event Signature: `0x2f8d2d194cbe1816411754a2fc9478a11f0707da481b11cff7c69791eb877ee1`

#### `SendWalletFees`[​](https://docs.kyberswap.com/Legacy/integrations/platform-fees#sendwalletfees) <a href="#sendwalletfees" id="sendwalletfees"></a>

Event is emitted when fees are sent to a wallet as part of the fee sharing program.

event **SendWalletFees**(address indexed wallet, address reserve, address sender)

| Parameter | Type    | Indexed | Description                        |
| --------- | ------- | ------- | ---------------------------------- |
| `wallet`  | address | YES     | reserve's specified wallet address |
| `reserve` | address | NO      | reserve's contract address         |
| `sender`  | address | NO      | sender's address                   |

Event Signature: `0xb3f3e7375c0c0c4f7dd94069a5a4e68667827491318da786c818b8c7a794924e`
