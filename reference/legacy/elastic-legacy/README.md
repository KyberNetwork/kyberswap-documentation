# Elastic Legacy

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

## Overview

On April 2023, KyberSwap received a bug report from a whitehat hacker notifying us of a vulnerability in our Elastic Legacy smart contracts which enabled liquidity deposits to be double-counted under a very specific scenario. Upon validating the bug report, KyberSwap immediately disabled new liquidity deposits and informed the community to remove all existing Elastic pool positions as a further safeguard to secure user funds. The timeline of events were as follow:

* 17 April 2023: Whitehat submitted bug report
* 17 April 2023: KyberSwap validated bug report
* 17 April 2023: KyberSwap announces potential vulnerability pending further investigation across [social channels](https://twitter.com/KyberNetwork/status/1647920799557505028?s=20) advising liquidity removals and that all user funds were safe. All Elastic Farming rewards were paused with an emergency withdrawal deadline set.
* 18 April 2023: KyberSwap [captures a snapshot](https://twitter.com/KyberNetwork/status/1648626138003181570) of remaining Elastic Farming positions and rewards. The snapshot will enable claim their allocated rewards in the future.
* 25 May 2023: KyberSwap releases Elastic with the vulnerability having been fixed and validated.

The audit reports for both Elastic Legacy as well as Elastic can be found on our [Audits](../../../security/audits.md) page.

While this situation was regrettable, there were many lessons which the KyberSwap team has carried forward to our current features. Most importantly, throughout this process, user funds remain SAFU and this user safety will always be front and center as we continue to introduce new and innovative features that empower KyberSwap users.

**This Elastic Legacy section will function as an archive of the documentation related to Elastic protocol and farms prior to the discovery of the vulnerability.**

You can view the post-mortem by the whitehat hacker [here](https://web.archive.org/web/20230524101408/https://100proof.org/kyberswap-post-mortem.html).
