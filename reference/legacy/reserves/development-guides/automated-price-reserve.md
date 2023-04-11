# Automated Price Reserve

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

In this guide, we will learn how to configure and deploy an Automated Price Reserve. Please note that the APR is centrally managed by the team setting it up and does not allow permissionless contribution. Should you wish to deploy or contribute liquidity to a permissionless AMM, kindly visit our [DMM guide](https://docs.kyberswap.com/Legacy/reserves/development-guides/reserves-dmm.md).

### Introduction[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#introduction) <a href="#introduction" id="introduction"></a>

The automated reserve was created with ease of maintenance as a top consideration. For the automated price reserve model, you rely on the smart contract and its predefined algorithm to automatically provide rates for the token being served liquidity for. In this model, you don't have gas, server, or development costs, but there is a learning curve and inability to control the rates in creative ways. This automated model only supports one token for one reserve. If you need to list another token using this model, another automated reserve must be deployed.

Moreover, the automated reserve was also designed to help discover the price of a newly created token that is previously not available in any centralized or decentralized exchange. Through the interaction of buyers and sellers, an estimated market price is discovered based on the market's sentiment at a point in time.

The automated reserve consists of only one component: an on-chain component of your reserve smart contracts that manages prices based on inventory.

The on-chain component has smart contracts that store your tokens, provide conversion rates, and swap your tokens with users. Since the smart contracts uses a pre-defined trading strategy based on initial parameters, the automated reserve automatically calculates the conversion rate. As a reserve manager, your primary purpose is to make sure that your automated reserve's ETH and token inventory is replenished when depleted. In the event of reserve depletion, you will need to deposit more ETH or tokens, and to set the parameters once again.

**Points to Note**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#points-to-note)

With this in mind, the automated reserve was designed with various parameters to help secure your funds.

* Prices are automatically updated based on a pre-defined algorithm as trades occur.
* A single buy or sell trade in ETH quantity does not go beyond the allowed max quantity cap parameter.
* Limited list of destination withdrawal addresses to prevent the operator account (hot wallet) from withdrawing funds to any destination address (if this account is compromised).
* **An automated price reserve can only support one token.** If another token needs to be supported, another automated price reserve needs to be deployed.

### Reserve Deployment and Setup[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#reserve-deployment-and-setup) <a href="#reserve-deployment-and-setup" id="reserve-deployment-and-setup"></a>

#### `Step 0: Clone Repo`[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#step-0-clone-repo) <a href="#step-0-clone-repo" id="step-0-clone-repo"></a>

Create a local directory, clone the `master` branch of our [reserves smart contracts repo](https://github.com/KyberNetwork/kyber\_reserves\_sc) and install necessary dependencies. Yarn is used as the package manager, but npm / npx can be used too.

```
git clone https://github.com/KyberNetwork/kyber_reserves_sc.git
cd kyber_reserves_sc
yarn install
yarn compile
```

#### `Step 1: Specifying Settings`[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#step-1-specifying-settings) <a href="#step-1-specifying-settings" id="step-1-specifying-settings"></a>

**Importing Private Key and Provider API**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#importing-private-key-and-provider-api)

We use the [Buidler](https://buidler.dev/) environment for deployment. Create a `.env` file in the root directory with the following settings:

```
INFURA_API_KEY=********************************
PRIVATE_KEY=0x****************************************************************
```

You can also specify other node provider API keys as well (eg. Alchemy, Metamask). Note that this means editing the `.hardhat.config.js` file too.

Navigate to the `./deployment/apr` directory and open `apr_input.json`, where you will the settings you have to define.

```json
{
  "tokenAddress": "0x4E470dc7321E84CA96FcAEDD0C8aBCebbAEB68C6",
  "whitelistedAddresses": ["0x5bab5ef16cfac98e216a229db17913454b0f9365"],
  "reserveAdmin": "0xBC33a1F908612640F2849b56b67a4De4d179C151",
  "reserveOperators": ["0x5bab5ef16cfac98e216a229db17913454b0f9365"],
  "pricingOperator": "0x5bab5ef16cfac98e216a229db17913454b0f9365",
  "outputFilename": "apr_reserve_deployment_details.json"
}
```

|        Property        |                                                                                        Explanation                                                                                       |
| :--------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|     `tokenAddress`     |              Token address on public testnets / mainnet. For local testnet environment, the deployer script can do token deployments as well, so you can ignore this field.              |
| `whitelistedAddresses` |                                                              Addresses that reserve operators can withdraw ETH and tokens to                                                             |
|     `reserveAdmin`     |                       Handles infrequent, manual operations like enabling trades on the reserve, and withdrawing funds to any account. Typically a **cold wallet**                       |
|   `reserveOperators`   | Used for withdrawing funds from the reserve to whitelisted addresses (e.g. when selling excess tokens in the open market. Typically **hot wallets**, and more than 1 operator is allowed |
|    `pricingOperator`   |                                  Used to set token prices whenever a reserve rebalance is needed. Recommended to be 1 of the reserve operator addresses                                  |

#### `Step 2: Deploying the contracts`[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#step-2-deploying-the-contracts) <a href="#step-2-deploying-the-contracts" id="step-2-deploying-the-contracts"></a>

The contracts to be deployed are the reserve and pricing contracts:

* `KyberReserve.sol`: The contract has no direct interaction with the end users (the only interaction with them is via the network platform). Its main interaction is with the reserve operator who manages the token inventory and feeds conversion rates to Kyber Network's contract.
* `LiquidityConversionRates.sol`: Provides the interface to set the liquidity parameters and the logic to maintain on-chain adjustment to the prices.

Run the command

```
yarn hardhat deployApr --network ropsten --network-address 0x920B322D4B8BAB34fb6233646F5c87F87e79952b
```

For more information on the arguments, run `yarn hardhat deployApr help`.

#### `Step 3: Test Deposits And Withdrawals`[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#step-3-test-deposits-and-withdrawals) <a href="#step-3-test-deposits-and-withdrawals" id="step-3-test-deposits-and-withdrawals"></a>

**Deposits**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#deposits)

Depositing funds into your reserve is easy. You can transfer ETH and tokens to your reserve contract from any address, like how you would with transferring funds for any ethereum wallet.

**Withdrawals**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#withdrawals)

Only authorized accounts have the right to withdraw tokens from the reserve.

* The reserve admin can call the `withdrawEther` and `withdrawToken` functions to withdraw tokens to any address.
* The reserve operator can only withdraw ether and tokens to whitelisted addresses by calling `withdraw`
* The reserve admin can add / remove whitelisted address by calling `approveWithdrawAddress`.

**Note:** It is recommended that you perform test deposits and withdrawals before proceeding to the next step.

#### `Step 4: Setting the liquidity parameters`[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#step-4-setting-the-liquidity-parameters) <a href="#step-4-setting-the-liquidity-parameters" id="step-4-setting-the-liquidity-parameters"></a>

The reserve manager needs to decide on the initial liquidity parameters of the automated reserve. The following parameters should be configured:

1. Initial ETH and Token Inventory Amounts
2. Initial Token Price `initialPrice`
3. Token Price Range
4. Maximum Buy and Maximum Sell Amount in a Trade
5. Fee Percentage

**About Token Price Range**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#about-token-price-range)

Unlike other AMM models that support unbounded price ranges, the reserve manager can specify the minium and maximum bounds that the reserve will fluctuate within. The limits on these bounds are dependent on the inventory amounts.

For example, a reserve manager can specify a maximum tolerance of 50% decrease and 100% increase relative to the initial token price. This is the default setting unless otherwise configured.

**Configuring liquidity parameters**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#configuring-liquidity-parameters)

Setting the liquidity parameters is done by executing the [`setLiquidityParameters()`](https://docs.kyberswap.com/Legacy/reserves/development-guides/api\_abi-liquidityconversionrates.md#setliquidityparams) function from the LiquidityConversionRates contract.

In the same `./deployment/apr` directory, open `liquidity_settings.json`. If you have completed step 2,the `reserve` field should have reflect the deployed reserve address.

```json
{
  "reserve": "0xcF76b605484Cd4bD46237c05B7De98d538ff44AE",
  "tokenPriceInEth": 0.00153086,
  "minAllowablePrice": 0.5,
  "maxAllowablePrice": 2,
  "maxTxBuyAmtEth": 10,
  "maxTxSellAmtEth": 10,
  "feePercent": 0.05
}
```

We explain the JSON fields in the table below:

|      Parameter      | Required |                                                                                 Explanation                                                                                |
| :-----------------: | :------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|      `reserve`      |    Yes   |                                                                               Reserve address                                                                              |
|  `tokenPriceInEth`  |    Yes   | Desired token price in ETH. For mainnet deployment, the script will fetch the latest price from CoinGecko. This behaviour can be disabled by passing a flag to the script. |
| `minAllowablePrice` |    No    |                            Maximum price decrease tolerable. Reserve returns 0 rate if price decreases further. Eg. 0.5 = 50% decrease in price                            |
| `maxAllowablePrice` |    No    |                            Maximum price increase tolerable. Reserve returns 0 rate if price increases further. Eg. 2.0 = 100% increase in price                           |
|   `maxTxBuyAmtEth`  |    No    |                                                          The maximum amount in ETH purchaseable in a single trade                                                          |
|  `maxTxSellAmtEth`  |    No    |                                                    The maximum token amount (specify in ETH) sellable in a single trade                                                    |
|     `feePercent`    |    No    |                                                           The fee amount that should be factored into the price.                                                           |

**Setting liquidity parameters**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#setting-liquidity-parameters)

**Things to note**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#things-to-note)

1. The correct network is specified (develop, ropsten, kovan, mainnet etc.)
2. The reserve has the desired ETH and token inventories, as the script will read the reserve's balances to calculate the right settings
3. Should the script throw some warnings, it is best to clarify these warnings with the Kyber team before proceeding to call `setLiquidityParams`.
4. If there are no warnings generated, and the private key specified in the `.env` file corresponds to the pricing operator, the script will automatically send a transaction to call `setLiquidityParams`.

**Testnets**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#testnets)

```
yarn hardhat setLiquidityParams --network ropsten --a false
```

The `-a` flag disables the price fetch behaviour.

**Mainnet**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#mainnet)

```
yarn hardhat setLiquidityParams --network mainnet --r "0xcF76b605484Cd4bD46237c05B7De98d538ff44AE"
```

The `-r` flag takes the reserve's address from the CLI instead of `liquidity_settings.json`.

```
yarn hardhat setLiquidityParams --network mainnet
```

#### `Step 5: Get your reserve authorized and running`[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#step-5-get-your-reserve-authorized-and-running) <a href="#step-5-get-your-reserve-authorized-and-running" id="step-5-get-your-reserve-authorized-and-running"></a>

Once you have completed the above steps, you can let any network operator know so that they can approve your reserve and list your token to the network. Kyber Network is currently the only network operator.

Once approved, you can test your reserve on [KyberSwap](https://ropsten.kyber.network/) Ropsten site! Please note that if there are other reserves listing same swap pair as you, your swap may not get matched with your reserve, because only the reserve that offers best rate will be matched. We can disable other reserves on the testnet to make sure you will swap with your reserve.

### Maintaining your APR[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#maintaining-your-apr) <a href="#maintaining-your-apr" id="maintaining-your-apr"></a>

This section walks you through the necessary steps involved in case you want to rebalance the APR or withdraw fees collected. You will also need to perform the same activities in the event that:

* the reserve is depleted of tokens or ETH;
* you want to rebalance your reserve;
* you want to withdraw fees from the reserve;
* when you want to change any of the liquidity parameters such as maximum buy/sell amount, initial price, etc.

**Note : It is highly recommended to follow the steps documented below to avoid incurring any loss of funds**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#note--it-is-highly-recommended-to-follow-the-steps-documented-below-to-avoid-incurring-any-loss-of-funds)

1. DISABLE trading in the reserve : The alerter can do this by calling `disableTrade()` function in the reserve contract.
2. Rebalance the reserve : After and only when the reserve is disabled, the reserve manager can deposit or withdraw Ether/Tokens to the reserve.
3. Recompute and set liquidity params. Run either `yarn hardhat setLiquidityParams --network mainnet` or `yarn hardhat setLiquidityParams --network mainnet --r <RESERVE_ADDRESS>`.
4. Enabling trading back : The admin can enable trades back by invoking the `enableTrade()` function in the reserve contract.

### Appendix[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#appendix) <a href="#appendix" id="appendix"></a>

#### Liquidity Params of `setLiquidityParams`[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#liquidity-params-of-setliquidityparams) <a href="#liquidity-params-of-setliquidityparams" id="liquidity-params-of-setliquidityparams"></a>

**About liquidity rate `r`**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#about-liquidity-rate-r)

`r` is liquidity the rate in basis points or units of 100 which the price should move each time the ETH/token inventory changes in 1 ETH worth of quantity. For an `r` of 0.007, the price will move 0.7% when buying / selling 1 Eth.

**About `pMin` and `pMax`**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#about-pmin-and-pmax)

With regards to the minimum/maximum supported price factor ratio, it is recommended to start with a ratio of 0.5:2.0. This indicates that the inventory will suffice for up to 100% increase or 50% decrease in token price with respect to ETH.

**Relationship between `r`, `initialPrice`, `E` and `pMin`**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#relationship-between-r-initialprice-e-and-pmin)

The initial token price determined by the pricing algorithm is as follows:

`initialPrice = minPrice * e^(r*E)` where `minPrice` = `pMin * initialPrice`

Rearranging the formula above, you find that `r = ln(initialPrice / minPrice) / E)` or `r = ln(1 / pMin) / E`

Hence, since the 4 variables are tightly coupled together, you are **only able to determine 3 out of these 4 variables, and use the formula to calculate the fourth.** Our recommendation is to **determine `initialPrice`, `E` and `pMin`, then calculate `r` using the above formula.**

**Graphical Illustration of Price adjustments**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#graphical-illustration-of-price-adjustments)

A quick overview of how price adjusts for a given price range can be seen below. This illustration uses 0.1, 70, 2 and 0.5 for the `intial price`, initial ETH amount `E`, `pMax` and `pMin` respectively.

![AprChart](https://docs.kyberswap.com/assets/images/aprchart-331fb1d8a33890c72798f9d0738c7867.png)

|  Type  |            Parameter            |                                                     Explanation                                                    |
| :----: | :-----------------------------: | :----------------------------------------------------------------------------------------------------------------: |
| `uint` |             `_rInFp`            |                                   r in formula precision, calculated as r \* Fp.                                   |
| `uint` |           `_pMinInFp`           | Minimum supported price in formula precision, calculated as min price factor \* initial price of your token \* Fp. |
| `uint` |           `_numFpBits`          |             The formula precision in bits, currently only 40 can be used, which gives precision of 2^40            |
| `uint` |        `_maxCapBuyInWei`        |                                   The allowed quantity for one BUY trade in ETH.                                   |
| `uint` |        `_maxCapSellInWei`       |                                   The allowed quantity for one SELL trade in ETH.                                  |
| `uint` |           `_feeInBps`           |                       The fee amount in basis points that should be calculated in the price.                       |
| `uint` | `_maxTokenToEthRateInPrecision` |     The maximum allowed price taking into consideration the maximum supported price factor. Units are in 10^18.    |
| `uint` | `_minTokenToEthRateInPrecision` |     The minimum allowed price taking into consideration the minimum supported price factor. Units are in 10^18.    |

**Example**[**​**](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#example)

Now, Let's assume we want to list a token with the following considerations:

1. Liquidity Rate – 0.007 (0.7%)
2. Initial Token Price – 1 token = 0.00005 ETH
3. Initial Ether Amount – 100 ETH
4. Initial Token Amount – 2,000,000 tokens (100 ETH worth)
5. Minimum (pMin) and Maximum (pMax) Supported Price Factor – 0.5:2.0
6. Maximum Buy and Maximum Sell Amount in a Trade – 5 ETH max buy and sell cap
7. Fee Percentage – 0.10%

Below, we will calculate the different parameters.

## Price Discovery Algorithm[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#price-discovery-algorithm)

How is the price be set, given a list of trades? Assuming the price (ETH/Token) will be given by _P(E)_ which will be a function of the current ETH reserve size. Then assuming we want a change in the price to be proportional to the amount traded we will have:

![AprFormula1](https://docs.kyberswap.com/assets/images/apr\_1-6bd106083c0f6ef3d25b0263d349da37.png)

where _r_ is the proportion factor. When _∆E_ is very small we'll have

<img src="../../../../.gitbook/assets/download.png" alt="" data-size="original">

integration gives

![AprFormula3](https://docs.kyberswap.com/assets/images/apr\_3-f52947ddd89e7795c7efaa73bfcea97b.png)\


Where _e^A_ is the minimal price given by _Pmin_ , so we have

![](<../../../../.gitbook/assets/download (1).png>)

The amount of tokens _Tmax_ that will be sold until reaching _Pmax_ , is related to the maximal price on our platform _P(Emax)_ in the following way

![](<../../../../.gitbook/assets/download (2).png>)

where _Emax_ is given from _Pmax_ itself,

![AprFormula6](https://docs.kyberswap.com/assets/images/apr\_6-970b912e134f5119b65689d0f3393f87.png)

carrying out the integration and plugging in _Emax_ will give:

![AprFormula7](https://docs.kyberswap.com/assets/images/apr\_7-693a86764d36a523709c03253245c038.png)

the initial amount of tokens _T0_ will be given by calculating _Tmax_ at _E0_ , which finally gives

![](<../../../../.gitbook/assets/download (3).png>)

similarly, the initial amount of ETH, E 0 , can be deduced from the initial price P 0 as

![](<../../../../.gitbook/assets/download (4).png>)

So given _Pmin_, _Pmax_, _P0_, _r_ we can find _E0_, _T0_, _Emax_.

#### Trading ∆E Ethers[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#trading-e-ethers) <a href="#trading-e-ethers" id="trading-e-ethers"></a>

_∆E_ can be positive (increasing the amount of ethers in the reserve and selling tokens to the trader), or negative. Solving the following integral

![AprFormula10](https://docs.kyberswap.com/assets/images/apr\_10-474a2e11ef4904a5395842806ee713a4.png)

will give the result for _∆T_

![AprFormula11](https://docs.kyberswap.com/assets/images/apr\_11-1cbf4704dc70d41ffaa8b50490795ba1.png)

#### Trading ∆T Tokens[​](https://docs.kyberswap.com/Legacy/reserves/development-guides/automated-price-reserve#trading-t-tokens) <a href="#trading-t-tokens" id="trading-t-tokens"></a>

_∆T_ can be positive (increasing the amount of tokens in the reserve and selling ethers to the trader), or negative. Integrating the following

![AprFormula12](https://docs.kyberswap.com/assets/images/apr\_12-065698173ad20a1a8d4a2be46a28d370.png)

and solving with respect to _∆E_ gives

\


<figure><img src="../../../../.gitbook/assets/download (5).png" alt=""><figcaption></figcaption></figure>

![AprChart](https://docs.kyberswap.com/assets/images/aprchart-331fb1d8a33890c72798f9d0738c7867.png)

The above figure shows the price function, with relevant parameters. _T0_ cannot be shown since its the area under _1/P_, not the area under _P_.
