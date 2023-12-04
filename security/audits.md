---
description: Committed To Security
---

# Audits

## Overview

Being open and permissionless, KyberSwap understands the importance of security in a hostile on-chain environment where smart contract code ultimately controls the flow of digital assets. As such, KyberSwap has proactively implemented multiple security measures in an effort to harden our protocol and governance contracts. This includes third-party audits, audit contests involving independent security experts from the wider community, as well as a consistently evolving bug bounty program.

***

## KyberSwap Elastic

### Third-party Audits

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>ChainSecurity - KyberSwap Elastic</strong></td><td></td><td><a href="../.gitbook/assets/Screenshot 2023-02-10 at 8.43.35 AM.png">Screenshot 2023-02-10 at 8.43.35 AM.png</a></td><td><a href="https://chainsecurity.com/security-audit/kyberswap-elastic/">https://chainsecurity.com/security-audit/kyberswap-elastic/</a></td></tr><tr><td><strong>ChainSecurity - KyberSwap Elastic Legacy</strong></td><td></td><td><a href="../.gitbook/assets/Audit_KyberSwapElasticLegacy (1).png">Audit_KyberSwapElasticLegacy (1).png</a></td><td><a href="https://chainsecurity.com/security-audit/kyberswap-elastic-legacy/">https://chainsecurity.com/security-audit/kyberswap-elastic-legacy/</a></td></tr></tbody></table>

ChainSecurity performed multiple audits of KyberSwap Elastic following additional security enhancements on the back of a vulnerability disclosure 17 months after Elastic's initial release in December 2021. The hardened Elastic contracts were deployed in May 2023 with no user funds lost during this upgrading process. The first iteration has been renamed to [Elastic Legacy](../reference/legacy/elastic-legacy/).

<table><thead><tr><th width="195"></th><th>Critical</th><th>High</th><th>Medium</th><th>Low</th></tr></thead><tbody><tr><td>Identified</td><td>0</td><td>1</td><td>0</td><td>6</td></tr><tr><td>Resolved</td><td>-</td><td>1</td><td>-</td><td>5</td></tr><tr><td>Risk Accepted</td><td>-</td><td>-</td><td>-</td><td>1</td></tr></tbody></table>

All findings for the latest KyberSwap Elastic 16 May 2023 audit were resolved with a single low risk being accepted:

* DOMAIN\_SEPARATOR Is Not Recomputed if chainId Changes -> Risk is isolated to cross-chain replay attacks in the event of the underlying chain forking.

Please refer to the full KyberSwap Elastic report linked above for further details.&#x20;

{% hint style="info" %}
**Elastic Legacy**

You can view the timeline and post-mortem of the whitehat disclosure and bounty [here](../reference/legacy/elastic-legacy/).
{% endhint %}

### Audit Contest

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Sherlock - KyberSwap Elastic</strong></td><td></td><td><a href="../.gitbook/assets/SherlockAudit.png">SherlockAudit.png</a></td><td><a href="https://audits.sherlock.xyz/contests/103">https://audits.sherlock.xyz/contests/103</a></td></tr></tbody></table>

In September 2023, an audit contest involving 207 participants from the Sherlock community was completed. The contest pot was open to any independent security experts who could identify vulnerabilities in the deployed Elastic contracts.&#x20;

| Issues submitted | Invalidated | High | Medium                 |
| ---------------- | ----------- | ---- | ---------------------- |
| 116              | 113         | 0    | 2  (1 duplicate issue) |

A total of 78,200 USDC was provided for 2 medium risk severities which was validated and scheduled **to be fixed in the next protocol deployment**:

* [UUPSUpgradeable vulnerability in OpenZeppelin Contracts](https://github.com/sherlock-audit/2023-07-kyber-swap-judging/issues/25) -> Vulnerability is restricted to a dependency package which can be mitigated through proper admin contract initialization which has been implemented for all deployed contracts. Dependency package has been fixed for all future deployments.
* [Router.sol is vulnerable to address collision](https://github.com/sherlock-audit/2023-07-kyber-swap-judging/issues/90) -> Address collision requires significant amount of computing power based on current hardware capabilities making such an attack infeasible in the short term.

Please refer to the [Sherlock contest details](https://audits.sherlock.xyz/contests/103) for further details and a full audit report.

{% hint style="warning" %}
**KyberSwap Elastic Exploit**

On 22 Nov 2023, there was an exploit that drained many liquidity pools. Our team is addressing the situation, and will keep you informed with regular updates via our public channels, such as [https://twitter.com/KyberNetwork](https://twitter.com/KyberNetwork). Meanwhile, KyberSwap Aggregator is not impacted and is operating as normal.

We urge all users to be vigilant against misinformation from malicious actors, and to not click on fake websites and phishing links. Our team will not DM you first. Thank you for your patience and understanding.
{% endhint %}

***

## KyberSwap Classic

### Third-party Audit

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>ChainSecurity - KyberSwap Classic</strong></td><td></td><td><a href="../.gitbook/assets/Screenshot 2023-02-10 at 8.40.35 AM.png">Screenshot 2023-02-10 at 8.40.35 AM.png</a></td><td><a href="https://chainsecurity.com/security-audit/kyberswap-classic/">https://chainsecurity.com/security-audit/kyberswap-classic/</a></td></tr></tbody></table>

ChainSecurity was engaged to conduct a code assessment of KyberSwap Classic with the final report published on 23 April 2021.

<table><thead><tr><th width="195"></th><th>Critical</th><th>High</th><th>Medium</th><th>Low</th></tr></thead><tbody><tr><td>Identified</td><td>0</td><td>0</td><td>4</td><td>6</td></tr><tr><td>Resolved</td><td>-</td><td>-</td><td>2</td><td>6</td></tr><tr><td>Risk Accepted</td><td>-</td><td>-</td><td>2</td><td>0</td></tr></tbody></table>

All audit findings were resolved with the reason for accepting the remaining medium risks as follows:

* Obsolete Storage Writes During Pool Deployment -> Only affects the gas costs of deploying new pools.
* Actual Amplification Reduces After Unblanced Contribution -> Attacker has no economic incentives for this attack vector and LPs will benefit from such a scenario.

Please refer to the full report linked above for additional details.

***

## KyberDAO & KNC

### Third-party Audit

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Hacken - KyberDAO &#x26; KNC</strong></td><td></td><td><a href="../.gitbook/assets/Screenshot 2023-03-07 at 9.12.22 AM.png">Screenshot 2023-03-07 at 9.12.22 AM.png</a></td><td><a href="https://hacken.io/audits/kyber-network/">https://hacken.io/audits/kyber-network/</a></td></tr></tbody></table>

Hacken was engaged to conduct an audit of the KNC token contract. There were no issues detected as part of the 18 May 2021 audit with the contract being rated as "Well-secured".

***

## Bug Bounty Program

In an effort to further secure the ecosystem, KyberSwap [officially launched](https://x.com/KyberNetwork/status/1690008019457748992?s=20) a bug bounty program on Immunefi on 11 August 2023. The bounty program covered multiple KyberSwap products including the Aggregator, Elastic, Limit Order, and the dApp interface.

Due to the recent Elastic exploit in Nov 2023, the program has been put on hold.
