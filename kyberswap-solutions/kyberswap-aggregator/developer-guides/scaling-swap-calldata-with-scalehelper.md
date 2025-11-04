---
description: For modifying effective amount in on-chain (at most ±5%)
---

# Scaling swap calldata with ScaleHelper

## Scale Helper contract

The getScaledInputData function is the main entry point for scaling swap transaction data. It takes pre-encoded transaction data for KyberSwap's MetaAggregationRouterV2 and adjusts the swap amount to a new value while maintaining all other parameters proportionally.

This function is essential for adjusting pre-built swap transactions when you need to change the input amount. For example, if you have encoded swap data for 100 tokens but want to swap 150 tokens instead, this function will scale all the internal amounts proportionally while maintaining the same swap route and parameters. The function returns false if the scaling fails (e.g., unsupported dexes, scaling constraints violated) and true with the new encoded data if successful. Thus it is important to specify onlyScalableSources=true when getting a route that needs to be scaled later.

### Interface

```solidity
function getScaledInputData(
    bytes calldata inputData,
    uint256 newAmount
  ) external view returns (bool isSuccess, bytes memory data);
```

### How to use

* **Parameters:**
  * `inputData`: The original `calldata` used to call `MetaAggregationRouterV2`.
  * `newAmount`: The new amount you want to adjust to.
* **Returns**
  * `isSuccess`: Indicates whether scaling was successful (`true`) or not (`false`).
  * `data`: The new `calldata` after scaling. You can use this directly with `MetaAggregationRouterV2`.
* **Example**
  * Before: RouterContract.call(inputData)
  * After: RouterContract.call(newScaledData)

## Contract address

* `0x2f577A41BeC1BE1152AeEA12e73b7391d15f655D`
* network support: eth, polygon POS, sonic, bnb, linea, mantle, bera, avax, arb, op, base, hyperEVM, ronin

## **📝 Usage Notes**

### **✅ Auto-scaling with Partial Support**

If the calldata includes multiple DEXes and only some support scaling:

* The contract will attempt to scale only the compatible DEX portions.
* This ensures the resulting calldata reflects the correct `newAmount` as best as possible.

### **⚠️ Handling Failures**

If scaling is **not** supported for the given calldata:

* `isSuccess` will be `false`.
* `data` will be empty.
* To prevent transaction reverts, you **should use `try-catch`** when calling the Scale Helper.

```solidity
try scaleHelper.getScaledInputData(inputData, newAmount) returns (bool success, bytes memory scaledData) {
    if (success) {
        // proceed with scaledData
    } else {
        // fallback to original or skip scaling
    }
} catch {
    // handle error case
}
```

### **🔒 Scaling Restrictions**

Some DEXes do not allow adjusting the input amount. So, if you attempt to scale with them, the function may return `false`.

To avoid including such DEXes, our API provides a parameter called [`onlyScalableSources`](https://docs.kyberswap.com/kyberswap-solutions/kyberswap-aggregator/aggregator-api-specification/evm-swaps). When set to `true`, the returned calldata will only include DEXes that:

* Support both scaling up and down
* Support scaling down only

Note: If you set `onlyScalableSources` to `true` and try to **scale up** with a DEX that only supports **scaling down**, it will return empty data.

The KyberSwap router also has restrictions on the maximum scaling allowed. The current limit is set at ±5% (95%–105%)

**Tip:**

* You can request calldata with a slightly higher amount (2–4%) than needed, then use the scale helper to scale it down accordingly.
* If you need to scale up more than 2%, it should exclude some sources:
  * native v1 + v2

### **🔧 Enable/Disable Scale Helper**

* Occasionally, we may upgrade or maintain the Scale contract, which could result in downtime. In such cases, we will contact you to disable the use of the Scale Helper. Therefore, integrators should implement a mechanism to disable scaling to avoid downtime issues.

### **💡 Upgradeability Notice**

* The Scale Helper contract is a **proxy**, meaning it can be upgraded in the future, but d**o not hardcode the contract address** in your integration. Instead, allow it to be configurable.
