# Token Quantity Conversion

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

### Token Amount Conversion[​](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#token-amount-conversion) <a href="#token-amount-conversion" id="token-amount-conversion"></a>

Since `getExpectedRate` returns a rate, not the amount, the following code snippets show how to convert to both source and destination token amounts, taking their decimals into account.

#### `calcSrcQty`[​](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#calcsrcqty) <a href="#calcsrcqty" id="calcsrcqty"></a>

| Parameter     |                        Description                        |
| ------------- | :-------------------------------------------------------: |
| `dstQty`      |       ERC20 destination token amount in its decimals      |
| `srcDecimals` |                ERC20 source token decimals                |
| `dstDecimals` |              ERC20 destination token decimals             |
| `rate`        | src -> dst conversion rate, independent of token decimals |

**Returns:**\
ERC20 source token amount in its decimals.

**Javascript**[**​**](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#javascript)

```
// DISCLAIMER: Code snippets in this guide are just examples and you
// should always do your own testing. If you have questions, visit our
// https://t.me/KyberDeveloper.

function calcSrcQty(dstQty, srcDecimals, dstDecimals, rate) {
  const PRECISION = 10 ** 18;
  //source quantity is rounded up. to avoid dest quantity being too low.
  if (srcDecimals >= dstDecimals) {
    numerator = PRECISION * dstQty * 10 ** (srcDecimals - dstDecimals);
    denominator = rate;
  } else {
    numerator = PRECISION * dstQty;
    denominator = rate * 10 ** (dstDecimals - srcDecimals);
  }
  return (numerator + denominator - 1) / denominator; //avoid rounding down errors
}
```

**Solidity**[**​**](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#solidity)

Refer to the [Utils contract](https://github.com/KyberNetwork/smart-contracts/blob/master/contracts/Utils.sol#L47-L64).

#### `calcDstQty`[​](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#calcdstqty) <a href="#calcdstqty" id="calcdstqty"></a>

| Parameter     |                        Description                        |
| ------------- | :-------------------------------------------------------: |
| `srcQty`      |         ERC20 source token amount in its decimals         |
| `srcDecimals` |                ERC20 source token decimals                |
| `dstDecimals` |              ERC20 destination token decimals             |
| `rate`        | src -> dst conversion rate, independent of token decimals |

**Returns:**\
ERC20 destination token amount in its decimals.

**Javascript**[**​**](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#javascript-1)

```
// DISCLAIMER: Code snippets in this guide are just examples and you
// should always do your own testing. If you have questions, visit our
// https://t.me/KyberDeveloper.

function calcDstQty(srcQty, srcDecimals, dstDecimals, rate) {
  const PRECISION = 10 ** 18;
  if (dstDecimals >= srcDecimals) {
    return (srcQty * rate * 10 ** (dstDecimals - srcDecimals)) / PRECISION;
  } else {
    return (srcQty * rate) / (PRECISION * 10 ** (srcDecimals - dstDecimals));
  }
}
```

**Solidity**[**​**](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#solidity-1)

Refer to the [Utils contract](https://github.com/KyberNetwork/smart-contracts/blob/master/contracts/Utils.sol#L34-L45).

#### `calcRateFromQty`[​](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#calcratefromqty) <a href="#calcratefromqty" id="calcratefromqty"></a>

| Parameter     |  Type  |                   Description                  |
| ------------- | :----: | :--------------------------------------------: |
| `srcAmount`   | Number |    ERC20 source token amount in its decimals   |
| `destAmount`  | Number | ERC20 destination token amount in its decimals |
| `srcDecimals` | Number |           ERC20 source token decimals          |
| `dstDecimals` | Number |        ERC20 destination token decimals        |

**Returns:**\
Token conversion rate independent of token decimals

**Javascript**[**​**](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#javascript-2)

```
// DISCLAIMER: Code snippets in this guide are just examples and you
// should always do your own testing. If you have questions, visit our
// https://t.me/KyberDeveloper.

function calcRateFromQty(srcAmount, destAmount, srcDecimals, dstDecimals) {
  const PRECISION = 10 ** 18;
  if (dstDecimals >= srcDecimals) {
    return (
      (destAmount * PRECISION) / (10 ** (dstDecimals - srcDecimals) * srcAmount)
    );
  } else {
    return (
      (destAmount * PRECISION * 10 ** (srcDecimals - dstDecimals)) / srcAmount
    );
  }
}
```

**Solidity**[**​**](https://docs.kyberswap.com/Legacy/api-abi/code-snippets/api\_abi-tokenquantityconversion#solidity-2)

Refer to the [Utils2 contract](https://github.com/KyberNetwork/smart-contracts/blob/master/contracts/Utils2.sol#L36-L49).
