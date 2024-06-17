# Zap Fee Model

## Fees model

There are two types of fees incorporated into the Zap API:

### **Protocol Fees**

Protocol fees are charged by KyberSwap in input token for Zap In feature, and are based on 4 different token pair categories:

| Pair Category   | Protocol Fee |
| --------------- | ------------ |
| Stable pair     | 0.01%        |
| Correlated pair | 0.025%       |
| Common pair     | 0.1%         |
| Exotic pair     | 0.25%        |

* Please refer to the example file below for a list of PancakeSwap v3 pools for each of the category above. PancakeSwap v3 pools not in the list belongs to the "Exotic pair" category.

{% file src="../../.gitbook/assets/zap_fee_pancakeswapv3.json" %}
Pair category for PancakeSwap V3 pools
{% endfile %}

### **Partner Fees**

* Partner fee configuration is sent by the partner client via the API to charge a partner fee on top of the protocol fees
* Similar to protocol fees, partners will only be able to charge the fee by the input token for Zap In.
* Provides both a valid non-zero feeAddress and a positive integer feePcm (the unit is per cent mille, i.e. 1-1000th of 1%) in the API call to [GetRoute](kyberswap-zap-as-a-service-zaas-api/zaas-http-api.md#get-route). Otherwise, no fee will be collected for partner.
