---
description: Conditional Liquidity Exit on Kyber Earn
---

# Smart Exit

## **Core Concept**

Providing liquidity allows users to earn trading fees, but it also introduces a key challenge: deciding when to exit a position. Liquidity providers often define an exit plan in advance, such as exiting at a target price, after earning a certain amount of fees, or at a specific time. Manually executing this strategy can be challenging due to market volatility and the need for constant monitoring.

Smart Exit addresses this challenge by allowing users to **predefine exit conditions and have their liquidity position exited automatically when those conditions are met**. This approach allows users to execute an exit strategy for a position without continuously monitoring market conditions or manually timing transactions. This represents a first-of-its-kind approach in the current LP management landscape for automating liquidity exit decisions.

### Technology and Its Components

Smart Exit adopts an **intent-based execution model**, where users declare exit conditions for a liquidity position instead of directly submitting an on-chain execution transaction. Rather than managing execution timing, gas fees, or transaction submission, users specify a set of conditions under which their liquidity should be exited.

These intent declarations are monitored **off-chain** for efficiency. When the specified conditions are satisfied, an execution transaction is generated and submitted for on-chain execution. At execution time, smart contracts validate that the transaction conforms to the user-defined intent before allowing the liquidity exit to proceed.

The system is **trustless and verifiable**. Although condition monitoring and transaction submission may involve off-chain components, all validation logic and execution constraints are enforced by public smart contracts. As a result, liquidity exits can only occur when the declared intent is satisfied, and execution behavior can be independently verified on-chain.

Smart Exit also supports **gasless execution**. Users are not required to hold native network tokens at the time of execution; instead, operators broadcast execution transactions on the user’s behalf. Despite this abstraction, execution and settlement remain fully on-chain and subject to smart contract validation.

