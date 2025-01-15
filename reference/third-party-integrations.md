# Third-Party Integrations

<details>

<summary>Transak</summary>

#### What is Transak?

Transak is a developer integration toolkit that enables onboarding of users to buy/sell crypto in any blockchain app, website or web plugin. Transak helps onboard mainstream users into dApp, protocol, game or wallet app.

#### Transak on [KyberSwap.com](http://kyberswap.com/)

Transak is integrated on KyberSwap through a browser integration that will redirect users to Transak to access their fiat on ramp services.

\*All of the KYC, regulation & compliance, fiat payment methods, and crypto coverage are solely handled by Transak.

Clicking "Buy Crypto" will bring you to a third party website, owned and operated by an independent party over which KyberSwap has no control ("[**Third Party Website**](https://global.transak.com/)").

For support, please contact Transak [**here**](https://support.transak.com/)**.**

Click here for more information on [**Transak**](https://docs.transak.com/docs/what-is-transak)

</details>

<details>

<summary>Axelar x Squid</summary>

#### What is Axelar?

Axelar delivers secure cross-chain communication for Web3, enabling you to build Interchain dApps that grow beyond a single chain. _Secure_ means Axelar is built on proof-of-stake, the battle-tested approach used by Ethereum, Polygon, Cosmos, and more. _Cross-chain communication_ means you can build a complete experience for your users that lets them interact with any asset, any application, on any chain with one click.

Click [**here**](https://docs.axelar.dev/) for more information on Axelar.

#### What is axlUSDC?

axlUSDC is a wrapped, multi-chain representation of USDC, a dollar stablecoin. For each unit of axlUSDC, there is a unit of USDC locked in an Axelar Gateway on Ethereum. axlUSDC is secured by a dynamic validator set running delegated Proof-of-Stake, which holds key shares in the Axelar Gateways via multi-party cryptography.

Click [**here**](https://docs.axelar.dev/learn/axlusdc) for more information on axlUSDC.

#### What is Squid?

Squid is the cross-chain swap and liquidity routing protocol on [Axelar Network](https://axelar.network/).&#x20;

Squid utilises existing DEXs to swap and send any native token between chains. This can be done via their SDK, Front End or Contracts directly.

Swaps are composable with Axelar's generalised message passing, so Squid can enable _one-click_ transactions between any application and any user, using any asset.&#x20;

Buy NFTs from any marketplace, use multi-chain DeFi, play a game on another chain, all without signing multiple transactions or downloading multiple wallets.

Click [**here**](https://docs.squidrouter.com/) for more information on Squid.

#### Why Axelar x Squid?

![](<../.gitbook/assets/Squid_LiquidityModel (1).jpg>)

By routing transactions through axlUSDC/USDC stable swap pools as well as USDC/native token pools, Squid supports swapping of any token combination across supported chains. Built on top of Axelar, Squid leverages Axelar's general cross-chain messaging abilities as well as its axlUSDC ecosystem to enable secure cross-chain token swaps.

#### Axelar x Squid on [KyberSwap.com](https://kyberswap.com/)

Squid is integrated on KyberSwap through API front end functionality to provide users with an option to conveniently swap tokens across the following supported chains:

* Ethereum (ChainID: 1)
* BSC (ChainID: 56)
* Arbitrum (ChainID: 42161)
* Polygon (ChainID: 137)
* Fantom (ChainID: 250)
* Avalanche (ChainID: 43114)

</details>

<details>

<summary>PayMaster x HoldStation</summary>

#### What is PayMaster?

Paymasters are smart contracts that able to pay gas fees for users. A Paymaster conversely, can sponsor transactions for users, enabling users to pay transaction fees in ERC20 tokens. This innovative approach to account management significantly enhances user experience, security, and flexibility, paving the way for broader adoption of blockchain technology.

The concept of paymasters, designed to enhance flexibility, user experience and transaction sponsorship in ERC-20 tokens, respectively. Despite some similarities with Ethereum's EIP 4337, key differences shape zkSync's unique account management approach.

To interact with a paymaster, EOA users sign their EIP-712 transaction.

Click [**here**](https://twitter.com/zksync/status/1595085984487837696?s=61\&t=dzZ-VSBCMZBnCBKauuc5Pg) for more information on PayMaster.

#### PayMaster powered by HoldStation on [KyberSwap.com](http://kyberswap.com/)

PayMaster is integrated on KyberSwap's Aggregator that will allow the users to access its account abstraction capabilities.

This development empowers KyberSwap users by offering the flexibility to pay gas fees using various tokens such as $USDC, $USDT, (wBTC TBA) and $HOLD&#x20;

![](<../.gitbook/assets/IMG_6812 (1).jpeg>)

One of the standout features of this launch is that users are no longer required to maintain ETH in their wallets. This enhancement simplifies the user experience and adds a new layer of convenience to the KyberSwap platform.

_Disclaimer:_ _The PayMaster module & contracts integrated on KyberSwap was developed and is operated by HoldStation. KyberSwap doesn't hold any responsibility over the feature._

</details>

<details>

<summary>BLINK</summary>

**What is Blink?**

Blink Protect [RPC](../getting-started/foundational-topics/decentralized-technologies/rpc.md) allows regular users to easily submit their transactions to the Blink Auction by using a custom RPC endpoint in their wallet. Everything should be the same for users, except transactions are sent to the Blink builder instead of the public mempool.

Endpoint: [https://ethereum-mev-protection.kyberengineering.io/](https://ethereum-mev-protection.kyberengineering.io/)

Key benefits to using the Blink RPC endpoint:

* **Frontrunning protection:** your transaction will not be seen by hungry sandwich bots in the public mempool.
*   **No failed transactions:** your transaction will only be included if it doesn't include any reverts, so you don't pay for failed transactions.

    > Note: your transaction could be uncled, emitted to the mempool, and then included on-chain.

Privacy notice: **Blink RPC does not track** any kind of user information (i.e. IP, location, etc.). No user information is ever stored or even logged.

Click [here](https://github.com/KyberNetwork/kyberswap-interface/commit/5ca7103e0099afe9c3e92fa0df7ed383fc03fdf3) for more information on Blink RPC.

**Blink on** [**KyberSwap.com**](https://kyberswap.com/swap/ethereum)

KyberSwap provides its user the option to conveniently connect to the Blink RPC when trading on the Ethereum mainnet.

</details>

<details>

<summary>Disclaimer on use of Third-party Integration/Service</summary>

For ease of communication, KyberSwap is referred to as "we" in this disclaimer. Any natural persons or other entities who engages in any activities on KyberSwap shall be considered as the user of KyberSwap, and is referred to as "you" in the disclaimer. We hereby remind you of the risks involved in using third-party services (referred to herein as “third-party services”).

1. Your use of any third-party services on KyberSwap is your personal decision and we have no control over it.
2. We are not responsible for the audit of any third-party services, nor do we make any commitments or guarantees on the validity, accuracy, correctness, reliability, quality, stability, completeness and/or timeliness of the technology and information involved in such third-party services and their associated services.
3. You are solely responsible for all outcomes arising from your choice to use the third-party services and their associated services.
4. You shall make your own judgement and evaluation as to whether any third-party services and its associated services comply with the applicable laws, regulations and relevant policy requirements of your jurisdiction. We do not provide any recommendation and opinions on this subject apart from recommending you to strictly abide by the laws and regulations of your jurisdiction.
5. Outcomes and occurrences which arise out of your use of any third-party services, including but not limited to legal issues, contract liability issues, and economic loss issues, shall be resolved between you and the relevant third-party services. We are not responsible for the resolution of any outcomes or disputes arising from your choice to use the third-party services.
6. We will not share any information with any third-party services unless under your consent. Once we receive your consent, you shall be solely responsible for all legal liabilities and disputes resulting from any third-party services access to your personal information and such labilities and disputes shall be resolved between you and the relevant third-party services.

**Our provision of access to third-party services on KyberSwap does not amount to any kind of recommendation, endorsement, or advice to use any third-party services or its associated services.**

</details>
