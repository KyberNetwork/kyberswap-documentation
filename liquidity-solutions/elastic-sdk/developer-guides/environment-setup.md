# Environment Setup

{% hint style="warning" %}
**KyberSwap Elastic Security Incident**

On 22 Nov 2023, the Elastic protocol experienced a security incident. More details can be found via our [official channels](https://x.com/KyberNetwork?s=20).

All other KyberSwap products ([Aggregator](../../../kyberswap-solutions/kyberswap-aggregator/), [Limit Order](../../../kyberswap-solutions/limit-order/), & [Classic](../../kyberswap-classic/)) continue to be fully operational.
{% endhint %}

## Overview

All of the sample code corresponding to specific operations can be found in the `/src/operations` folder in the demo repo below:

{% embed url="https://github.com/KyberNetwork/ks-sdk-elastic-demo" %}

To get the test environment up and running, you can run the following:

```
git clone https://github.com/KyberNetwork/ks-sdk-elastic-demo.git
npm install
npm run start // Run once
npm run start:dev // Run on save (Nodemon)
```

## Provider And Signer Setup

In order for our application to communicate with the blockchain, we will first need to specify a [provider](https://docs.ethers.org/v6/api/providers/#Provider) as well as a [signer](https://docs.ethers.org/v6/api/providers/#Signer).

From [Ethers.js Docs](https://docs.ethers.org/v6/getting-started/):

{% tabs %}
{% tab title="Provider" %}
A [Provider](https://docs.ethers.org/v6/api/providers/#Provider) is a read-only connection to the blockchain, which allows querying the blockchain state, such as account, block or transaction details, querying event logs or evaluating read-only code using call.

If you are coming from Web3.js, you are used to a Provider offering both read and write access. In Ethers, all write operations are further abstracted into another Object, the Signer.
{% endtab %}

{% tab title="Signer" %}
A [Signer](https://docs.ethers.org/v6/api/providers/#Signer) wraps all operations that interact with an account. An account generally has a private key located somewhere, which can be used to sign a variety of types of payloads.

The private key may be located in memory (using a [Wallet](https://docs.ethers.org/v6/api/wallet/#Wallet)) or protected via some IPC layer, such as MetaMask which proxies interaction from a website to a browser plug-in, which keeps the private key out of the reach of the website and only permits interaction after requesting permission from the user and receiving authorization.
{% endtab %}
{% endtabs %}

The examples utilize KyberSwap's own [RPC provider](https://polygon.kyberengineering.io/) for Polygon PoS but you configure your preferred provider in the [`provider.ts`](https://github.com/KyberNetwork/ks-sdk-elastic-demo/blob/main/src/libs/provider.ts) file. For simplicity, the Ethers [Wallet](https://docs.ethers.org/v6/api/wallet/) instance was used to directly sign outgoing transactions using an imported private key specified in [`signer.ts`](https://github.com/KyberNetwork/ks-sdk-elastic-demo/blob/main/src/libs/signer.ts).

{% hint style="warning" %}
**Importing private keys**

Your private keys are required for signing transactions which will result in changes to the blockchain state (i.e. token transfers, swaps, etc.). To avoid the complexity of frontend interfaces, the examples implements the Elastic operations in a pure Node.js environment thereby requiring your private keys to be imported.

You will need to replace the `MATIC_PRIVATE_KEY` constant with your own private key in order to execute trade and liquidity management operations. To export your private key from Metamask, open Metamask and go to Account Details > Export Private Key.

**NEVER EXPOSE YOU PRIVATE KEYS (i.e. gommit to a public repo) AS ANYONE WITH YOUR KEYS WILL BE ABLE TO ACCESS YOUR ASSETS.**
{% endhint %}

## Important Folders And Files

### /src/index.ts

Starting point for code execution. For each Elastic operation, a corresponding function has been created in the `index.ts` file.  To execute a specific operation, please uncomment the relevant function.&#x20;

### /src/operations/

Contains individual `.ts` files that corresponds to each operation.&#x20;

### /src/libs/constants.ts

Specifies various constants that are required for the operation:

* Tokens
* Contract Addresses

### /src/libs/provider.ts

Ethers.js provider configuration which specifies the chain as well as [provider](https://docs.ethers.org/v5/api/providers/).

### /src/libs/signer.ts

Ethers.js provider configuration which specifies the wallet which contains the [signer methods](https://docs.ethers.org/v5/api/signer/) required to execute a write operation.

### /src/libs/abis/

Contains the various Elastic smart contract [ABI](https://docs.soliditylang.org/en/latest/abi-spec.html) definitions.
