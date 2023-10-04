# Environment Setup

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

### /src/libs/abis/

Contains the various Elastic smart contract [ABI](https://docs.soliditylang.org/en/latest/abi-spec.html) definitions.
