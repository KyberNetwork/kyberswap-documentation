# RESTful API Overview

{% hint style="warning" %}
You are referring to the **`Legacy`** version of KyberSwap docs.

For the most updated information, please refer to:

* [**`Classic`**](../../../../liquidity-solutions/kyberswap-classic/)
* [**`Elastic`**](../../../../liquidity-solutions/kyberswap-elastic/)
* [**`Limit Order`**](../../../../kyberswap-solutions/limit-order/)
* [**`Aggregator`**](../../../../kyberswap-solutions/kyberswap-aggregator/)
{% endhint %}

### Introduction[​](https://docs.kyberswap.com/Legacy/api-abi/restful-api/api\_abi-restfulapioverview#introduction) <a href="#introduction" id="introduction"></a>

The RESTful API can be used to perform trades on the Kyber Network platform.

#### NETWORK URL[​](https://docs.kyberswap.com/Legacy/api-abi/restful-api/api\_abi-restfulapioverview#network-url) <a href="#network-url" id="network-url"></a>

| Network |                                   URL                                   |
| :-----: | :---------------------------------------------------------------------: |
| Mainnet |         [https://api.kyber.network](https://api.kyber.network/)         |
| Ropsten | [https://ropsten-api.kyber.network](https://ropsten-api.kyber.network/) |

### Things to note[​](https://docs.kyberswap.com/Legacy/api-abi/restful-api/api\_abi-restfulapioverview#things-to-note) <a href="#things-to-note" id="things-to-note"></a>

If for any reason there is an error in the response, you will receive the following response message:

```json
{
    “error”:True,
    ”reason”:””,
    ”additional_data”:””
}
```

The `reason` can be one of the following:

* `**request_limit**`: indicates that the user exceeded the requests limit
* `**param_error**`: indicates that the user has passed an unknown parameter, a wrong type for that parameter, or has not passed a required parameter
* `**server_error**`: indicates internal API error, which should not be present most of the time

`additional_data` will contain more information on the error, such as indicating when the user can request again in case of “request\_limit”, or indicating bad or missing parameters for `param_error`.

Please ensure that errors are being handled appropriately. For example, if you get an error when calling the `tradeData` endpoint, ensure that your users are not able to proceed with the trade.

#### REST Limitations[​](https://docs.kyberswap.com/Legacy/api-abi/restful-api/api\_abi-restfulapioverview#rest-limitations) <a href="#rest-limitations" id="rest-limitations"></a>

There is a current limitation of **60 requests per minute per IP address**. If you exceed this you will get the following reply:

```json
{
    “error”: True,
    ”reason”: “request_limit”,
    ”additional_data”: “Retry in 60 seconds”
}
```

If requests are still continually sent after receiving this error, then the requests sent from your IP will be silently blocked. It will take approximately an one hour of not sending a request from the blocked IP to be removed from the blocked list.
