# Slippage Rate Protection

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

### Safeguarding Users From Slippage Rates[​](https://docs.kyberswap.com/Legacy/integrations/slippage-rate-protection#safeguarding-users-from-slippage-rates) <a href="#safeguarding-users-from-slippage-rates" id="safeguarding-users-from-slippage-rates"></a>

The token conversion rate varies with different source token quantities. It is important to highlight the slippage in rates to the user when dealing with large token amounts. We list some methods on how this can be done below.

#### Method 1: Reject the transaction if the slippage rate exceeds a defined percentage[​](https://docs.kyberswap.com/Legacy/integrations/slippage-rate-protection#method-1-reject-the-transaction-if-the-slippage-rate-exceeds-a-defined-percentage) <a href="#method-1-reject-the-transaction-if-the-slippage-rate-exceeds-a-defined-percentage" id="method-1-reject-the-transaction-if-the-slippage-rate-exceeds-a-defined-percentage"></a>

1. Call `getExpectedRate` for 1 ETH equivalent worth of `srcToken`.
2. Call `getExpectedRate` for actual `srcToken` amount.
3. If the obtained rates differ by a defined percentage (either in the smart contract, or as a user input), reject the transaction.

#### Method 2: Display rate slippage in the user interface[​](https://docs.kyberswap.com/Legacy/integrations/slippage-rate-protection#method-2-display-rate-slippage-in-the-user-interface) <a href="#method-2-display-rate-slippage-in-the-user-interface" id="method-2-display-rate-slippage-in-the-user-interface"></a>

<figure><img src="https://docs.kyberswap.com/assets/images/showing-slippage-rate-7ee9fcae6a397578a47f6302ac729a74.jpeg" alt=""><figcaption></figcaption></figure>

&#x20;An example of how this could be done is shown above. How the rate slippage is calculated is as follows:

1. Call `getExpectedRate` for 1 ETH equivalent worth of `srcToken`.
2. Call `getExpectedRate` for actual `srcToken` amount.
3. Calculate the rate difference and display it **prominently** in the user interface.

### Slippage rates when using `maxDestAmount`[​](https://docs.kyberswap.com/Legacy/integrations/slippage-rate-protection#slippage-rates-when-using-maxdestamount) <a href="#slippage-rates-when-using-maxdestamount" id="slippage-rates-when-using-maxdestamount"></a>

In the case where `maxDestAmount` is being used, beware of slippage rates when `maxDestAmount` is significantly lower than `srcQty`. We give an example below.

1. Users wants to swap for a `maxDestAmount` of 3000 DAI, but specifies a `srcQty` of 300 ETH.
2. Kyber will search the best rate for the `srcQty` of 200 ETH, but the rate might be significantly worse than rates for lower `srcQty`. For example, the user gets a rate of 1 ETH = 100 DAI, while he could have gotten a better rate of 1 ETH = 200 DAI if he specified a lower `srcQty`.
3. Kyber will use the rate to calculate the amount necessary for 2900 DAI, and refund the rest of the unused ETH back to the user. In the case mentioned above, 30 ETH will be used, and the remaining 270 ETH returned to him. He could have instead needed just half that amount (15 ETH) had he specified a lower `srcQty` instead.

In summary, if `srcQty` is significantly larger than `maxDestAmount`, the user could potentially be forced to trade with significantly worse rates.
