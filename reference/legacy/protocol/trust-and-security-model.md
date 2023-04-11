# Trust and Security Model

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

### Who should the users trust?[​](https://docs.kyberswap.com/Legacy/trust-security-model#who-should-the-users-trust) <a href="#who-should-the-users-trust" id="who-should-the-users-trust"></a>

The users are not required to trust anyone because the protocol does not hold their funds (only when a trade is being executed). Additionally, being entirely on-chain allows users to freely verify and audit the smart contracts. For added security, a multisig wallet is used for executing admin actions.

Users can also specify a minimum conversion rate to prevent a trade from executing in the event slippage causes the conversion rate of a trading pair to fall below the minimum rate specified.

If users trade with Kyber via an affiliate’s interface, they have to check the transaction parameters, especially the _platform fee_ charged, because there are no safeguards or sanity checks in the proxy contract.

### Who should reserve managers trust?[​](https://docs.kyberswap.com/Legacy/trust-security-model#who-should-reserve-managers-trust) <a href="#who-should-reserve-managers-trust" id="who-should-reserve-managers-trust"></a>

The reserves are required to trust the Kyber Network administrators not to perform malicious actions such as:

* Disabling trades without good rationale
* Change the MatchingEngine contract code such that the fairness in the selection of reserves for trades is affected
* Setting reserve rebates to zero without clear communication and coordination.

In addition, the reserve managers should be aware that their reserves could be affected by extreme market conditions like flash crashes or from sub-optimal inventory management (e.g. setting wrong prices or from large exposure to risky tokens).

### Who should Kyber trust?[​](https://docs.kyberswap.com/Legacy/trust-security-model#who-should-kyber-trust) <a href="#who-should-kyber-trust" id="who-should-kyber-trust"></a>

Kyber Network administrators need to read smart contracts of the reserves and tokens in order to list them on the network contract. They need to ensure that the token contract is not malicious, for example.

### Who should affiliates trust?[​](https://docs.kyberswap.com/Legacy/trust-security-model#who-should-affiliates-trust) <a href="#who-should-affiliates-trust" id="who-should-affiliates-trust"></a>

Affiliates have to trust Kyber not to set a malicious Kyber Network. For example, a network that doesn’t send the platform fees to the FeeHandler.
