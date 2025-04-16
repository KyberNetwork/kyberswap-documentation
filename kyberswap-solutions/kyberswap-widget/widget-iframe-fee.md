---
description: >-
  Users trading directly on KyberSwap.com UI are not subject to this fee
  structure.
---

# Widget/iFrame Fee

## Overview

The Widget/iFrame fee structure is **not applied universally across all integrations**; it depends on the specific protocols using it. These fees are not technically charged by KyberSwap—instead, they are configured by the partner protocols themselves. KyberSwap provides the underlying infrastructure that enables these protocols to implement and manage their own customizable fee structures.

Users trading directly on [KyberSwap.com](http://kyberswap.com/) UI are not subject to this fee structure.

## **Fee Visibility**

When executing a swap using the Widget/iFrame, the applicable transaction (platform) fee is shown in the swap details section, when you get the route **and** before you confirm the transaction.\
If no Platform Fee is configured, it will not be displayed.

<figure><img src="../../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>

## Fee Collection Mechanism

KyberSwap offers a flexible underlying infrastructure that enables partners and protocols to collect the Widget/iFrame Fee in either the input or output token of each swap. Additionally, partners can customize the fee structure according to their specific needs by choosing between a percentage of the trade size or a fixed token amount. Upon successful execution of the swap, the fee is directly transferred to the specified `feeReceiver` address (provided as one of the parameters).

<details>

<summary><strong>Example of choosing Fee Token:</strong></summary>

A. When Both Tokens Are Listed in the Token Catalog

1.  Stable Token Priority:

    If either the input or output token is a stablecoin, the stablecoin will be used as the fee token.

    If both are stable coin, the higher rank on CMC will be used as the fee token.

    If neither are the stable coin, the process moves to the next step.
2. Native Token Priority:
   *   If either token is a native token:

       When either the input or the output token is the native token on the network being used, that native token is automatically chosen as the fee token.
   *   If neither token in nor token out is native:

       The process moves to the next step.
3. Whitelisted Token Check:
   *   Only one token whitelisted:

       If one token is marked as whitelisted (i.e., recognized or preferred by the protocol) and the other is not, the whitelisted token is chosen.
   *   Both tokens are either whitelisted or not whitelisted:

       The fee token is then determined based on the ranking of each token:

       *   Ranking Method:

           The tokens are first compared using their CoinMarketCap (CMC) ranking, which reflects their market capitalization position.

           * If no CMC ranking is available for a token, the protocol uses an alternative ranking (CGK Rank).
           * If both tokens are whitelisted and one token does not have a valid ranking while the other does, the token with the available ranking will be selected as the fee token.
       *   Decision:

           The token with the better (higher) ranking is designated as the fee token.

B. When One or Both Tokens Are Not Listed in the Token Catalog

1. Only One Token Listed:
   * The listed token is chosen as the fee token.
2. Neither Token Listed:
   * The fee token defaults to the input token.

</details>



{% hint style="success" %}
*   **Service-Specific Application:**

    The fee structure detailed above applies solely to **swap** transactions executed on some protocols using the Widget/iFrame. It **does not apply universally** and does not apply to other services such as Zap, Limit Order, or any other services provided by KyberSwap.
*   **Direct Platform Exclusion:**

    Users trading **directly on the** [**KyberSwap.com**](http://kyberswap.com) **UI are not subject to this fee structure**, as a separate set of fee configurations governs transactions on the main platform.
{% endhint %}
