---
description: Earn Rewards For Governance Participation
---

# Voting

<details>

<summary>How do I vote?</summary>

Voting in KyberDAO happens fully on the Ethereum blockchain. If you stake KNC in epoch “n”, you will be eligible to vote in epoch “n+1” (next epoch onwards).

<img src="https://kyber.org/static/media/faq7.b02361d2.png" alt="" data-size="original">

Connect your Ethereum wallet, and go to the Vote tab. You will see the current proposals which you can vote on.

Weigh your given options, make your choice, and click “Submit vote“. Kindly note that once voting is successful, you may CHANGE your vote, but you won’t be able to REMOVE your vote.

</details>

<details>

<summary>How long does a proposal last?</summary>

It depends, for less critical (short timelock) proposals, it takes approximately 4 days of voting, while for more critical (long timelock) proposals, it takes approximately 7 days. Proposals have to start and end within the same epoch.

</details>

<details>

<summary>Do I need ETH / gas to vote?</summary>

Yes, vote submission is done on-chain. As such, you have to pay for the cost of making that on-chain transaction.

</details>

<details>

<summary>Can I appoint someone to vote for me?</summary>

Yes, you can delegate your voting power to someone else e.g. a friend’s address. Once you have staked KNC, you have an option for delegation. You have to delegate your full KNC stake (no partial delegation) and can only delegate your KNC to one Ethereum address at any time. Stakers who delegate their KNC stake are also known as voting pool members.

Reminder: If you stake KNC in epoch “n”, you or your delegate will only be eligible to vote in epoch “n+1” (next epoch onwards).

Step 1: On the Stake KNC page → Select Delegate tab

Step 2: Connect your wallet

Step 3: Paste the Ethereum address that you want to delegate voting power to → Click ‘Delegate’

Important: In this default delegation method, your delegate is responsible for voting on your behalf and distributing your KNC rewards to you (though your delegate can’t touch or withdraw your own staked KNC). Kyber Network does not hold your funds or manage this process. KyberDAO voting is operated using the blockchain and is fully transparent and verifiable.

![](<../../../.gitbook/assets/image (82).png>)

</details>

<details>

<summary>How does KyberDAO determine the power of each vote?</summary>

Your voting power is determined by the amount of KNC you have staked, in proportion to the total amount of KNC staked in the KyberDAO and used for voting on proposals.

</details>

<details>

<summary>Is voting transparent? How do we know the result is accurate and fair?</summary>

Yes, the voting process is fully transparent. Since voting is an on-chain operation, it will have a transaction hash and other details that will be available for anyone to review on etherscan. Results are achieved through a democratic process - proposal options with the highest voting points win.

Once the proposal campaign period is over, votes submitted are considered final. But there is a delay period prior to the execution of the proposal to provide time for the Kyber community and DAO maintainer to highlight any major issues. For less critical (short timelock) proposals, the delay is 12 hours, while for more critical (long timelock) proposals, the delay is 7 days.

For the latest governance parameters, please read [https://github.com/KyberNetwork/KIPs/blob/master/KIPs/kip-19.md](https://github.com/KyberNetwork/KIPs/blob/master/KIPs/kip-19.md).

</details>

<details>

<summary>How are voting and rewards linked?</summary>



2 simple rules: \
(A) You MUST VOTE to get the reward, and (B) You must vote in ALL the ongoing proposals to get your full reward for that particular epoch.

If the epoch has 2 proposals, but you voted in only 1 proposal, you will get only half of your rewards.

</details>

<details>

<summary>How are voting rewards APR calculated?</summary>

The voting rewards APR % is calculated based on the following formula:

$$VoteAPR = \frac{\text{Total KNC Rewards}}{\text{Average KNC Voted In KIPs}}*\frac{365}{\text{TimePeriod}_\text{days}}$$

Note that the time period used starts from the beginning of the epoch when the KIP was proposed to the reward distribution date.

Calculation is based on rewards distributed to KNC voters since KIP21.

</details>

<details>

<summary>How do I claim rewards?</summary>

On the Vote page [https://kyberswap.com/kyberdao/vote](https://kyberswap.com/kyberdao/vote), connect your Ethereum wallet, and go to the Your Voting Reward tab. You are able to view all your unclaimed rewards and claim them.

To be eligible for 100% of your share of the rewards, you need to have staked KNC, participate in every DAO vote, and have your KNC staked for the entire epoch.

If you have delegated your voting power to someone else, your delegate must have voted on your behalf. It is up to your delegate to distribute rewards to you.

</details>

<details>

<summary>What currency are rewards distributed in?</summary>

Rewards are distributed in KNC. Trading fees collected from KyberSwap trading activity are in the form of LP (liquidity provider) tokens which are subsequently converted to KNC at an appropriate time to be distributed to voters.

</details>

<details>

<summary>When can I claim my rewards?</summary>

Stakers can claim their eligible rewards from previous epochs whenever they want. In general, rewards are generated after every 1-2 epochs (2-4 weeks), assuming you have voted in the previous epochs. If you delegate your vote to someone else, it is up to them to decide how often they want to distribute rewards to you.

</details>

<details>

<summary>Do I get rewards if I don’t vote?</summary>

No. You have the option to delegate your vote to a friend or 3rd party KyberDAO pool operator (e.g. Unagii) who can vote on your behalf, collect rewards, and distribute rewards to you.

</details>
