# iFrame Alternative

## Overview

KyberSwap provides an iFrame option for integrators that require swap functionality to be embedded directly into their website or dApp.&#x20;

{% hint style="success" %}
#### Note on integrations: clientID and domain whitelisting

In order to ensure the security of user's fund when interacting with the KyberSwap iFrame, KyberSwap requires integrator domains to be whitelisted. By doing so, integrators can protect their users from cross-domain attacks.&#x20;

**Please contact our Head of BD, `sasha@kyber.network`,  if you would like to get your domain whitelisted. Upon whitelisting, you will then be provided with the base domain for iFrame integration.**

To accompany the domain, KyberSwap also implements a `clientId` field that enables us to continuously improve the KyberSwap Widget by understanding how swaps are being utilized. As a developer integrating with our widget, **please add your clientID (i.e. company name) to the `clientId` field** to enable us to serve you better.
{% endhint %}

## Parameters

<table><thead><tr><th width="199.33333333333331">Params</th><th width="125">Required</th><th>Description</th></tr></thead><tbody><tr><td>clientId</td><td>Yes</td><td>ID of the client integrating the iFrame.</td></tr><tr><td>chainId</td><td>No</td><td>The chainId for the transaction. Full list can be found <a href="../../getting-started/supported-exchanges-and-networks.md">here</a>.</td></tr><tr><td>inputCurrency</td><td>No</td><td>The token that the user is selling.</td></tr><tr><td>outputCurrency</td><td>No</td><td>The token that the user is buying.</td></tr><tr><td>features</td><td>No</td><td>Token swap mode(s) to enable in iFrame. Separated by <code>,</code>.<br><br><code>swap</code>: Market order facilitated by the <a href="../kyberswap-aggregator/">KyberSwap Aggregator</a>.<br><br><code>limit</code>: Limit order facilitated by <a href="../limit-order/">KyberSwap Limit Order</a>.<br><br><code>cross-chain</code>: Cross-chain swaps facilitated by <a href="../kyberswap-interface/user-guides/swap-between-different-tokens-across-chains.md">Squid and KyberSwap</a>.</td></tr><tr><td>tab</td><td>No</td><td>Token swap mode to be loaded when iFrame is first loaded.</td></tr><tr><td>feeReceiver</td><td>No</td><td>Address to receive fee (if <code>chargeByFee</code> is not empty)</td></tr><tr><td>feeAmount</td><td>No</td><td>Fee amount to be collected<br><br>If <code>isInBps</code> = <code>true</code>, <code>feeAmount</code> is the % of fees that we will take with base unit = 10000 (i.e. <code>feeAmount</code> = 10 and <code>isInBps</code> = <code>true</code> then fee = 0.1%)<br><br>If <code>isInBps</code> = <code>false</code>, <code>feeAmount</code> is the amount of tokens that we will take as fees (i.e. <code>feeAmount</code>=10 and <code>isInBps</code> = <code>false</code> then fee = 10 wei)</td></tr><tr><td>isInBps</td><td>No</td><td>If true, fee is taken in BPS</td></tr><tr><td>chargeFeeBy</td><td>No</td><td>Indicates whether fee is charged by input token <code>inputCurrency</code> or output token <code>outputCurrency</code>. <br><br>Default is empty whereby no fee is charged.</td></tr></tbody></table>

## Adding the iFrame to your site

Sample code:

```jsx
    <iframe
      style={{ margin: 'auto' }}
      width="500px"
      height="900px"
      src="{customDomain}?clientId={yourClientId}&tab=swap&inputCurrency=ETH&outputCurrency=0xe4DDDfe67E7164b0FE14E218d80dC4C08eDC01cB&isInBps=1&chargeFeeBy=currency_in&feeReceiver=0xDcFCD5dD752492b95ac8C1964C83F992e7e39FA9&feeAmount=500&chainId=42161"
    />
```
