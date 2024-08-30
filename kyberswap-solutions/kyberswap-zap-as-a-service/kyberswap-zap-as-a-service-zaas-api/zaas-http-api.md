---
description: HTTP API doc for ZaaS API
---

# ZaaS HTTP API

{% file src="../../../.gitbook/assets/zap_service.yaml" %}
OpenAPI YAML
{% endfile %}

Please refer to the following server configuration and openapi file for the http API.

## Common Parameters

| Configuration        | Value                                                                                                                                                                                                                            |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Base URL             | <ul><li><code>https://zap-api.kyberswap.com/{chain}</code> where chain is one of the <a href="../zaps-supported-chains-dexes.md">supported chain</a>. For example: <code>https://zap-api.kyberswap.com/arbitrum</code></li></ul> |
| Header `X-Client-Id` | <p>Some value to identify your client.</p><p>Please contact <a href="mailto:bd@kyber.network">bd@kyber.network</a> to whitelist your client id with more rate limit quota</p>                                                    |

## API list

### Zap in

#### Get Route

{% swagger src="../../../.gitbook/assets/zap_service.yaml" path="/api/v1/in/route" method="get" %}
[zap_service.yaml](../../../.gitbook/assets/zap_service.yaml)
{% endswagger %}

{% tabs %}
{% tab title="Bash" %}
```bash
curl -X GET "https://zap-api.kyberswap.com/polygon/api/v1/in/route?dex=DEX_UNISWAPV3&pool.id=0xb46388f104ff88aac68626a316aaf3a924f32055&position.tickLower=-24800&position.tickUpper=32400&tokenIn=0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE&amountIn=1000000000000000000&slippage=100" \
 -H "accept: application/json"\
 -H "x-client-id: zap-docs"
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
fetch('https://zap-api.kyberswap.com/polygon/api/v1/in/route?dex=DEX_UNISWAPV3&pool.id=0xb46388f104ff88aac68626a316aaf3a924f32055&position.tickLower=-24800&position.tickUpper=32400&tokenIn=0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE&amountIn=1000000000000000000&slippage=100', {
  headers: {
    'accept': 'application/json',
    'x-client-id': 'zap-docs'
  }
});
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

headers = {
    'accept': 'application/json',
    'x-client-id': 'zap-docs',
}

params = {
    'dex': 'DEX_UNISWAPV3',
    'pool.id': '0xb46388f104ff88aac68626a316aaf3a924f32055',
    'position.tickLower': '-24800',
    'position.tickUpper': '32400',
    'tokenIn': '0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE',
    'amountIn': '1000000000000000000',
    'slippage': '100',
}

response = requests.get('https://zap-api.kyberswap.com/polygon/api/v1/in/route', params=params, headers=headers)
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require 'net/http'

uri = URI('https://zap-api.kyberswap.com/polygon/api/v1/in/route?dex=DEX_UNISWAPV3&pool.id=0xb46388f104ff88aac68626a316aaf3a924f32055&position.tickLower=-24800&position.tickUpper=32400&tokenIn=0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE&amountIn=1000000000000000000&slippage=100')
req = Net::HTTP::Get.new(uri)
req['accept'] = 'application/json'
req['x-client-id'] = 'zap-docs'

req_options = {
  use_ssl: uri.scheme == 'https'
}
res = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
  http.request(req)
end
```
{% endtab %}
{% endtabs %}

#### Build Route

{% swagger src="../../../.gitbook/assets/zap_service.yaml" path="/api/v1/in/route/build" method="post" %}
[zap_service.yaml](../../../.gitbook/assets/zap_service.yaml)
{% endswagger %}

{% tabs %}
{% tab title="Bash" %}
```bash
curl -X POST "https://zap-api.kyberswap.com/polygon/api/v1/in/route/build" \
 -H "accept: application/json"\
 -H "content-type: application/json"\
 -H "x-client-id: zap-docs" \
 -d '{"sender":"0x0d500B1d8E8eF31E21C99d1Db9A6444d3ADf1270","recipient":"0x5cb738DAe833Ec21fe65ae1719fAd8ab8cE7f23D","route":"KLUv/WALBWUVAKavgSFAb9qflX03+n9Wj9hEtiy3sD717uBIcklIUtb9UBVFASZwAG8AewCseGGDZz+f91M98txGAZqZqQsXPJhqdXGMHUIosW9O3X9D9ykvz587bZntFA+ybObckq051tD33d6immunvvu1fJ584ZaJB7tzeUH7jBfGkjJLmzw1GHNfFpS6uHNC7SJxoQMzFkbw7EKHR7EubGBGFDwMD76LRM+krFq9qkyNUC9kEi1HIhRHC7BQ8iwgDMREw9E88FRyoQUe3d1X1WmZdd13nzPVJkbpFzKe9ImUFau7UkkdoU7rrkob/cLF8yr1lzvRdntKumohg+d/c1MyvypzJ3ZnVvmqUP/CCZ4MFRR4b3mPgEmai5fykypW/M+uUGc6UqjV+vaERXQuLpywCFTMSWW+a2rki1JyJv301E6EuKEkvAnDloWPaYxxsAqB13BIFJo3IWEHB3k7n1FCrqvSKw5wk4ZUrp6p7OnTanbzoEAo2KPg8SYgEsWHb+4OUMcV4GmAOiwMlcrDQ6WC3tilpdQOpUrWinl/I8SaO19ljaGwCjy58OK5R0HTdAWK0Cu13SgoCBMNCNMGIhgMvlCiiXg8g4PuNRIRjmcBsBUAktd4MIa1iAeTaFy8CLOY4HlIKM1baBwUDqZ/XfvWqSrba5ma77q5X5V6i/o178ZAIBHMcHBY+BoKRIInQCBAAkOIkfEBRAi1htoyA+Fh2bFWvRh8hvz97PowAKx1qdsQ5xjp2pgs22UIOyQAShdlhjfwZzCdB+z1ohnGvFnSTTKxnORd4epZFuIeA+w2wAw7LgAorNLwQsqNf+xgg82V4vgsD37S9QzcQQb7FtadgPK3lKx7U4HBskxWQGuCP0HydKwMJ+YSsBBVIoM2YptDA0F2jZS8pJQuID3loJeJAg==","deadline":1800000000,"source":"zap-docs"}' 
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
fetch('https://zap-api.kyberswap.com/polygon/api/v1/in/route/build', {
  method: 'POST',
  headers: {
    'accept': 'application/json',
    'content-type': 'application/json',
    'x-client-id': 'zap-docs'
  },
  body: JSON.stringify({
    'sender': '0x0d500B1d8E8eF31E21C99d1Db9A6444d3ADf1270',
    'recipient': '0x5cb738DAe833Ec21fe65ae1719fAd8ab8cE7f23D',
    'route': 'KLUv/WALBWUVAKavgSFAb9qflX03+n9Wj9hEtiy3sD717uBIcklIUtb9UBVFASZwAG8AewCseGGDZz+f91M98txGAZqZqQsXPJhqdXGMHUIosW9O3X9D9ykvz587bZntFA+ybObckq051tD33d6immunvvu1fJ584ZaJB7tzeUH7jBfGkjJLmzw1GHNfFpS6uHNC7SJxoQMzFkbw7EKHR7EubGBGFDwMD76LRM+krFq9qkyNUC9kEi1HIhRHC7BQ8iwgDMREw9E88FRyoQUe3d1X1WmZdd13nzPVJkbpFzKe9ImUFau7UkkdoU7rrkob/cLF8yr1lzvRdntKumohg+d/c1MyvypzJ3ZnVvmqUP/CCZ4MFRR4b3mPgEmai5fykypW/M+uUGc6UqjV+vaERXQuLpywCFTMSWW+a2rki1JyJv301E6EuKEkvAnDloWPaYxxsAqB13BIFJo3IWEHB3k7n1FCrqvSKw5wk4ZUrp6p7OnTanbzoEAo2KPg8SYgEsWHb+4OUMcV4GmAOiwMlcrDQ6WC3tilpdQOpUrWinl/I8SaO19ljaGwCjy58OK5R0HTdAWK0Cu13SgoCBMNCNMGIhgMvlCiiXg8g4PuNRIRjmcBsBUAktd4MIa1iAeTaFy8CLOY4HlIKM1baBwUDqZ/XfvWqSrba5ma77q5X5V6i/o178ZAIBHMcHBY+BoKRIInQCBAAkOIkfEBRAi1htoyA+Fh2bFWvRh8hvz97PowAKx1qdsQ5xjp2pgs22UIOyQAShdlhjfwZzCdB+z1ohnGvFnSTTKxnORd4epZFuIeA+w2wAw7LgAorNLwQsqNf+xgg82V4vgsD37S9QzcQQb7FtadgPK3lKx7U4HBskxWQGuCP0HydKwMJ+YSsBBVIoM2YptDA0F2jZS8pJQuID3loJeJAg==',
    'deadline': 1800000000,
    'source': 'zap-docs'
  })
});
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

headers = {
    'accept': 'application/json',
    'content-type': 'application/json',
    'x-client-id': 'zap-docs',
}

json_data = {
    'sender': '0x0d500B1d8E8eF31E21C99d1Db9A6444d3ADf1270',
    'recipient': '0x5cb738DAe833Ec21fe65ae1719fAd8ab8cE7f23D',
    'route': 'KLUv/WALBWUVAKavgSFAb9qflX03+n9Wj9hEtiy3sD717uBIcklIUtb9UBVFASZwAG8AewCseGGDZz+f91M98txGAZqZqQsXPJhqdXGMHUIosW9O3X9D9ykvz587bZntFA+ybObckq051tD33d6immunvvu1fJ584ZaJB7tzeUH7jBfGkjJLmzw1GHNfFpS6uHNC7SJxoQMzFkbw7EKHR7EubGBGFDwMD76LRM+krFq9qkyNUC9kEi1HIhRHC7BQ8iwgDMREw9E88FRyoQUe3d1X1WmZdd13nzPVJkbpFzKe9ImUFau7UkkdoU7rrkob/cLF8yr1lzvRdntKumohg+d/c1MyvypzJ3ZnVvmqUP/CCZ4MFRR4b3mPgEmai5fykypW/M+uUGc6UqjV+vaERXQuLpywCFTMSWW+a2rki1JyJv301E6EuKEkvAnDloWPaYxxsAqB13BIFJo3IWEHB3k7n1FCrqvSKw5wk4ZUrp6p7OnTanbzoEAo2KPg8SYgEsWHb+4OUMcV4GmAOiwMlcrDQ6WC3tilpdQOpUrWinl/I8SaO19ljaGwCjy58OK5R0HTdAWK0Cu13SgoCBMNCNMGIhgMvlCiiXg8g4PuNRIRjmcBsBUAktd4MIa1iAeTaFy8CLOY4HlIKM1baBwUDqZ/XfvWqSrba5ma77q5X5V6i/o178ZAIBHMcHBY+BoKRIInQCBAAkOIkfEBRAi1htoyA+Fh2bFWvRh8hvz97PowAKx1qdsQ5xjp2pgs22UIOyQAShdlhjfwZzCdB+z1ohnGvFnSTTKxnORd4epZFuIeA+w2wAw7LgAorNLwQsqNf+xgg82V4vgsD37S9QzcQQb7FtadgPK3lKx7U4HBskxWQGuCP0HydKwMJ+YSsBBVIoM2YptDA0F2jZS8pJQuID3loJeJAg==',
    'deadline': 1800000000,
    'source': 'zap-docs',
}

response = requests.post('https://zap-api.kyberswap.com/polygon/api/v1/in/route/build', headers=headers, json=json_data)
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require 'net/http'
require 'json'

uri = URI('https://zap-api.kyberswap.com/polygon/api/v1/in/route/build')
req = Net::HTTP::Post.new(uri)
req.content_type = 'application/json'
req['accept'] = 'application/json'
req['x-client-id'] = 'zap-docs'

req.body = {
  'sender' => '0x0d500B1d8E8eF31E21C99d1Db9A6444d3ADf1270',
  'recipient' => '0x5cb738DAe833Ec21fe65ae1719fAd8ab8cE7f23D',
  'route' => 'KLUv/WALBWUVAKavgSFAb9qflX03+n9Wj9hEtiy3sD717uBIcklIUtb9UBVFASZwAG8AewCseGGDZz+f91M98txGAZqZqQsXPJhqdXGMHUIosW9O3X9D9ykvz587bZntFA+ybObckq051tD33d6immunvvu1fJ584ZaJB7tzeUH7jBfGkjJLmzw1GHNfFpS6uHNC7SJxoQMzFkbw7EKHR7EubGBGFDwMD76LRM+krFq9qkyNUC9kEi1HIhRHC7BQ8iwgDMREw9E88FRyoQUe3d1X1WmZdd13nzPVJkbpFzKe9ImUFau7UkkdoU7rrkob/cLF8yr1lzvRdntKumohg+d/c1MyvypzJ3ZnVvmqUP/CCZ4MFRR4b3mPgEmai5fykypW/M+uUGc6UqjV+vaERXQuLpywCFTMSWW+a2rki1JyJv301E6EuKEkvAnDloWPaYxxsAqB13BIFJo3IWEHB3k7n1FCrqvSKw5wk4ZUrp6p7OnTanbzoEAo2KPg8SYgEsWHb+4OUMcV4GmAOiwMlcrDQ6WC3tilpdQOpUrWinl/I8SaO19ljaGwCjy58OK5R0HTdAWK0Cu13SgoCBMNCNMGIhgMvlCiiXg8g4PuNRIRjmcBsBUAktd4MIa1iAeTaFy8CLOY4HlIKM1baBwUDqZ/XfvWqSrba5ma77q5X5V6i/o178ZAIBHMcHBY+BoKRIInQCBAAkOIkfEBRAi1htoyA+Fh2bFWvRh8hvz97PowAKx1qdsQ5xjp2pgs22UIOyQAShdlhjfwZzCdB+z1ohnGvFnSTTKxnORd4epZFuIeA+w2wAw7LgAorNLwQsqNf+xgg82V4vgsD37S9QzcQQb7FtadgPK3lKx7U4HBskxWQGuCP0HydKwMJ+YSsBBVIoM2YptDA0F2jZS8pJQuID3loJeJAg==',
  'deadline' => 1800000000,
  'source' => 'zap-docs'
}.to_json

req_options = {
  use_ssl: uri.scheme == 'https'
}
res = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
  http.request(req)
end
```
{% endtab %}
{% endtabs %}
