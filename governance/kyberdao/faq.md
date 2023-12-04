---
description: Your KyberDAO Questions Answered
---

# FAQ - Others

## General

<details>

<summary>Which Ethereum wallet connections are supported? </summary>

Metamask, Ledger, Trezor, JSON keystore file, Coinbase Link, and WalletConnect are supported.

</details>

<details>

<summary>How does KyberDAO fund voting rewards?</summary>

Currently, 10% of the KyberSwap fees collected from trades through liquidity pools are sent to KyberDAO to be used as voting rewards (the other 90% goes to liquidity providers).

KyberDAO converts the fees collected into KNC tokens which are then distributed as rewards to KNC holders who stake and vote. This aligns incentives between KNC holders and KyberSwap adoption, and allows for a positive loop where KNC holders have the ability to easily stake KNC again for additional voting power and rewards.

The current fee ratio between KyberDAO and liquidity providers was approved by a KIP-8 vote. This fee ratio may change in the future, subject to a new KyberDAO vote. If and when that happens, this article will be updated accordingly.

</details>

<details>

<summary>What is "block time"?</summary>

The time between two blocks of the validated chain (Ethereum in the case of KyberDAO). It’s approximately 15-16 seconds for Ethereum blockchain.

</details>

<details>

<summary>What is an "epoch"?</summary>

An epoch is a time period. KyberDAO operations are divided into epochs. For example: proposals for voting can be submitted within a duration of 1 epoch, which is about 2 weeks.

Within an epoch, for less critical (short timelock) proposals, it requires approximately 4 days of voting, while for more critical (long timelock) proposals, it takes approximately 7 days. Proposals have to start and end within the same epoch.

</details>

<details>

<summary>How secure are KyberSwap and KyberDAO?</summary>

Kyber Network highly values the security of the KyberSwap protocol and the KyberDAO governance platform.

KyberSwap is fully non-custodial and our users’ funds are not held by KyberSwap. In addition, KyberSwap, KyberDAO, and their associated smart contracts have been audited by reputable audit teams in the blockchain industry, such as [Chainsecurity](https://chainsecurity.com/) and [Hacken](https://hacken.io/).

You can refer to the [Audits](../../security/audits.md) page for the respective reports.

</details>

## Staking and voting

Please refer to the [Staking](user-guides/staking.md) or [Voting](user-guides/voting.md) pages for further details.

<details>

<summary>How do i stake KNC in KyberDAO?</summary>

To stake KNC, you just need an Ethereum wallet that holds KNC tokens. Note that only KNC on the Ethereum network can be staked since the DAO smart contracts are on the Ethereum network.

Please refer to [Participating in KyberDAO](user-guides/participating-in-kyberdao.md) for a step-by-step guide.

</details>

<details>

<summary>What is a delegation/staking service?</summary>

Delegation or Staking services are 3rd party entities that help KNC stakers cast votes on their behalf and help them earn staking rewards. Some services like unagii.com allow KNC holders to stake directly on their platform.

Simple delegation to another Ethereum address is done on: [https://kyberswap.com/kyberdao/stake-knc](https://kyberswap.com/kyberdao/stake-knc)

Example: Alice staked 1000 KNC and delegated her voting power to her friend Bob’s Ethereum address. Bob casts votes on Alice’s behalf. KNC rewards will be distributed to Bob’s Ethereum address. Bob takes his commission (he can also choose to do it for free) and transfers the remaining rewards to Alice. Note that although KNC rewards will be given to Bob after he votes, Bob cannot touch or withdraw Alice’s staked KNC. Alice has full control over her staked KNC.\
\
Important: In this simple delegation method, your delegate is responsible for voting on your behalf and distributing your KNC rewards to you, though only you can withdraw/unstake your own KNC. Kyber Network does not hold your funds or manage this process.

</details>

<details>

<summary>What is the delegation fee?</summary>

The percentage of KNC voting rewards that 3rd-party delegation/staking services can choose to keep in exchange for voting on your behalf or providing other delegation services. This is up to the external delegation service and not managed by Kyber Network.

There is no charge when you manually stake and vote on your own (without using a 3rd-party service) on the default KyberDAO interface on KyberSwap.com

</details>

<details>

<summary>Do I need to run a node to stake?</summary>

No. Just connect your Ethereum wallet on KyberSwap.com and stake KNC there.

</details>

<details>

<summary>Is there any ‘slashing’ involved like other staking systems?</summary>

No. You will always be able to withdraw the full KNC capital deposited.

</details>

<details>

<summary>What is "Total Staked" and "Current Epoch Votes"?</summary>

“Total Staked KNC” means how much of the total KNC supply is currently staked on KyberDAO. Currently, KNC has a total supply of about \~223.4M. If total KNC staked is \~40M KNC, it means about 18% of the total supply is staked.

“Total Voting Rewards” represents the amount of KNC rewards that have been collected (from converting a portion of KyberSwap trading fees) to be distributed to eligible voters.

</details>

## KNC

<details>

<summary>KNC token contract address</summary>

#### KNC Address

KNC is the ticker symbol for Kyber Network Crystal v2, the native token of KyberSwap that is used by our governance DAO, KyberDAO. The KNC token address is `0xdeFA4e8a7bcBA345F687a2f1456F5Edd9CE97202`

#### KNCL Address

KNCL is the ticker symbol for Kyber Network Crystal v1, our legacy token that can and should be migrated to KNC as soon as possible. For a guide on how to migrate KNCL to KNC, please refer to [this blogpost](https://blog.kyber.network/knc-token-migration-guide-fda08bfe62c2). The KNCL token address is `0xdd974d5c2e2928dea5f71b9825b8b646686bd200`

</details>

<details>

<summary>How to migrate KNCL to KNC v2</summary>

#### Introduction

In KIP-6, the Kyber team proposed a Kyber Network Crystal (KNC) token upgrade and migration to make KNC much more dynamic and flexible with the ability to support more efficient upgrades, while amplifying KyberDAO’s governance power. The KyberDAO community gave their strong stamp of approval with a large majority of 99.89% voting in favor of the proposal.

The [old token](https://etherscan.io/address/0xdd974d5c2e2928dea5f71b9825b8b646686bd200) (aka Kyber Network Crystal Legacy or KNCL) can now be migrated to the [new KNC token](https://etherscan.io/address/0xdeFA4e8a7bcBA345F687a2f1456F5Edd9CE97202) using our migration portal.

#### How to Migrate

Migration can be performed via the migration portal at [https://kyberswap.com/kyberdao/stake-knc](https://kyberswap.com/kyberdao/stake-knc)&#x20;

**Step 1**: Connect your wallet to KyberSwap and ensure that you are on the Ethereum network.

**Step 2**: Open the migration portal UI by clicking on this link:

<img src="https://support.kyberswap.com/hc/article_attachments/15982987237401" alt="mceclip0.png" data-size="original">

**Step 3**: If this is the first time you're performing migration, you will first need to approve your wallet's KNCL balance for use. Click "Approve" to do so. This is a one-time onchain transaction that will require gas fees.

<img src="https://support.kyberswap.com/hc/article_attachments/15983089053977" alt="mceclip1.png" data-size="original">

Once the approval step is complete, the "Migrate" button should appear.

**Step 4**: Specify the amount of KNCL to migrate. You can either do so by manually typing in an amount or by using the "Max" and "Half" buttons. Click "Migrate" to proceed. This is an onchain transaction that will require gas fees.

<img src="https://support.kyberswap.com/hc/article_attachments/15983280856089" alt="mceclip2.png" data-size="original">

The migration transaction should now appear on your transaction history.

<img src="https://support.kyberswap.com/hc/article_attachments/15983405613721" alt="mceclip3.png" data-size="original">

</details>

## Troubleshooting

<details>

<summary>KyberDAO cannot see my KNC balance</summary>

If you have a positive KNC balance but [KyberDAO](https://kyberswap.com/kyberdao/stake-knc) cannot find your balance even though your wallet is connected, please ensure that your network is set to **Ethereum** and that you have a **positive ERC20 KNC token balance**. The DAO is on the Ethereum network, so you will only be able to stake KNC that is on the Ethereum network.

<img src="https://support.kyberswap.com/hc/article_attachments/14345621843993" alt="KyberDAO_Balance_Network.png" data-size="original">

If you have KNC tokens on other networks, these will first need to be [bridged to Ethereum](broken-reference) before they can be used to participate in KyberDAO.

</details>

<details>

<summary>What if I have more questions?</summary>

Join Kyber’s official [Discord Server](https://discord.com/invite/kyberswap) and the [KyberDAO Twitter](https://twitter.com/kyberdao) account for the latest updates.

</details>
