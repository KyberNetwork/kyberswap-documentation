---
description: Auto-compounding single-asset strategies on Kyber Earn
---

# Partner Vaults

## Introduction

#### **What are Partner Vaults?**

Partner Vaults are single-asset, auto-compounding strategy vaults operated by third-party protocols and made accessible through Kyber Earn. You deposit one asset, and the partner protocol allocates it across a set of DeFi positions and rebalances according to that vault's strategy.

At launch, Partner Vaults are provided by [ether.fi](https://etherfi.gitbook.io/etherfi) through its Liquid vaults (more partner vaults will come soon).

{% hint style="info" %}
Kyber Earn does not operate Partner Vaults or manage their strategies. Deposited assets are held in the partner protocol's vault contracts. Returns are variable and not guaranteed.
{% endhint %}

#### **What can you do with a Partner Vault on Kyber Earn?**

Kyber Earn adds token routing on top of the partner protocol's vaults. That changes three things about how you use them:

* **Compare vaults and liquidity pools side by side.** Both opportunity types appear in Kyber Earn, so a single-asset vault and a concentrated liquidity position can be evaluated against each other before you commit.
* **Deposit with any single or multiple tokens.** Fund a position from one or multiple tokens you already hold; Kyber Earn converts and deposits in a single transaction, rather than requiring you to acquire the vault's deposit asset first.
* **Exit to any token without waiting.** Vault positions can be converted directly into another token in one transaction, instead of waiting out the partner protocol's withdrawal queue. The amount received is set by market pricing rather than the vault's redemption value.

#### **How do Vaults differ from liquidity pools?**

Both are ways to put assets to work through Kyber Earn, but they behave differently:

<table><thead><tr><th width="169.97265625"></th><th>Liquidity Pools</th><th>Vaults</th></tr></thead><tbody><tr><td>Entry</td><td>Up to 5 tokens, within a chosen price range</td><td>One or more tokens, converted into the vault's deposit asset through Zap. No price range</td></tr><tr><td>Yield source</td><td>Trading fees and reward programs (if available)</td><td>Strategy allocation across DeFi positions</td></tr><tr><td>Impermanent loss</td><td>Applies</td><td>Not applicable — single-asset exposure</td></tr><tr><td>Earnings</td><td>Claimed or compounded per position</td><td>Compounded automatically into your balance</td></tr><tr><td>Exit</td><td>Immediate, via Standard Withdrawal or Zap Out</td><td>Through the partner's withdrawal queue, or by swapping to another token</td></tr><tr><td>Managed by</td><td>Liquidity Provider</td><td>The partner protocol</td></tr><tr><td>Smart Exit</td><td>Supported</td><td>Not supported</td></tr></tbody></table>

{% hint style="info" %}
Partner Vaults are operated and managed by [ether.fi](https://ether.fi/) or other protocols. KyberSwap provides the access interface and token routing only, and does not control, operate, or guarantee the performance of any Partner Vault. Any vault-related concerns should be directed to the partner protocol.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2026-09-25 at 12.24.05.png" alt=""><figcaption></figcaption></figure>

**Ready to start?** Browse the available vaults, compare their APY and TVL, and open any vault to see what its strategy does before you commit: [https://kyberswap.com/earn/vaults](https://kyberswap.com/earn/vaults), or choose Earn > Explore Vaults from the menu.

**Want to understand the mechanism?** Each vault is operated by its partner protocol, which decides how deposits are allocated and rebalanced. For [ether.fi](https://ether.fi/) vaults, see their documentation: [https://etherfi.gitbook.io/etherfi](https://etherfi.gitbook.io/etherfi).

#### Withdrawal options

Kyber Earn offers two withdrawal methods, which differ in speed and in how your output is priced.

<table data-header-hidden><thead><tr><th width="147.17578125"></th><th></th><th></th></tr></thead><tbody><tr><td></td><td><strong>Withdraw to any token</strong></td><td><strong>Native withdrawal</strong></td></tr><tr><td>Timing</td><td>Single transaction, settles immediately</td><td>Processed through a queue, typically several days</td></tr><tr><td>Claiming</td><td>Not required. Tokens arrive in your wallet in the same swap transaction</td><td>Not required. Tokens are sent to your wallet automatically when the request completes</td></tr><tr><td>You receive</td><td>Any supported token</td><td>The vault's underlying asset</td></tr><tr><td>Pricing</td><td>On-chain price</td><td>The vault's share redemption value</td></tr></tbody></table>

**Withdraw to any token** converts your vault shares directly into a token of your choice in a single transaction, with no waiting period. The conversion is routed through KyberSwap Aggregator, which searches across liquidity sources for the rate available at that moment.

Before you confirm, you see the estimated amount you will receive, the minimum guaranteed after slippage, and any price impact. Because this method prices at the market rather than redeeming at the vault's share value, the amount you receive may be higher or lower than a native withdrawal.

<figure><img src="../../.gitbook/assets/Screenshot 2026-09-25 at 16.51.58.png" alt=""><figcaption></figcaption></figure>

**Native withdrawal** submits a redemption request to [ether.fi](https://ether.fi/)'s withdrawal queue and returns the vault's underlying asset. It is not immediate and can take several days; the processing time is shown before you confirm. Your request moves through Requested, Pending, and Completed states, visible on your vault position. When it completes, the assets are sent to your wallet automatically — there is no claim step.

<figure><img src="../../.gitbook/assets/Screenshot 2026-09-25 at 12.26.50.png" alt=""><figcaption></figcaption></figure>
