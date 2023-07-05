---
description: Rest API End Points
---

# REST API

### <mark style="color:blue;">Overview</mark>

| Chain                    | Base Url                              |
| ------------------------ | ------------------------------------- |
| Arbitrum Goerli (421613) | https://test.orderbook.premia.finance |
| Arbitrum One (42161)     | https://orderbook.premia.finance      |

Users can access the [`GET` quotes](rest-api.md#get-quotes) and [`POST` quotes](rest-api.md#publish-quotes) methods of the REST API _directly_ using the `/quotes` end-point.  Additionally, for users who have requested an RFQ quote, the quotes returned can be accessed via [`GET` rfq\_quotes](rest-api.md#get-rfq\_quotes).  In order to use REST API endpoints, you must also pass in an [API KEY](./#api-key). &#x20;

### <mark style="color:blue;">Publish Quotes</mark>

{% swagger src="../../.gitbook/assets/openapi.yaml" path="/quotes" method="post" %}
[openapi.yaml](../../.gitbook/assets/openapi.yaml)
{% endswagger %}

#### Example:

```javascript
import fetch from 'cross-fetch';
import { parseEther } from 'ethers';

const url = 'https://test.orderbook.premia.finance/quotes'

// Free or Paid Tier API KEY
const MOCK_API_KEY = '3423ee2bfd89491f82b351404ea8c3b7'

// object array of one or more quotes
const mockQuotes = [{
  poolKey: {
    base: '0x9f5D1212514Ac88E26c523387C60F87B67AD1130',
    quote: '0x53421DB1f41368E028A4239954feB5033C7B3729',
    oracleAdapter: '0xB89756634Bae979d13721d9883e67CF22cc31D6b',
    strike: parseEther('2900').toString(),
    maturity: 1688716800,
    isCallPool: false
  },
  chainId: '421613'
  provider: '0x9E600587b9035a8C1254E8256F4E588CC33B8467',
  taker: '0x0000000000000000000000000000000000000000',
  price: parseEther('.195').toString(),
  size: parseEther('1').toString(),
  isBuy: false,
  deadline: 1686592096,
  salt: 1686584896,
  signature: {
    r: '0x7feff79a77a023fd8e034066c5bdb78e9b9e5e3804dfc02c0d5b3979b5be8324',
    s: '0x58229484d69566752b48c49326e6eaca2b4fba5372ba638870bda5b58b4fb25e',
    v: 28
  }
}]


async publishQuote(quotes) {
  const response = await fetch(url, {
      method: 'POST',
      headers: {
          'Content-Type': 'application/json',
          'x-apikey': MOCK_API_KEY,
      },
      body: JSON.stringify(quotes),
  })
  
  if (!response.ok) {
    console.error('Request failed: ', await response.json())
    throw new Error(`Failed to publish quotes: ${response.statusText}`)
  }
		
  return response.json()
}


publishQuote(mockQuotes)
```

### <mark style="color:blue;">Get Quotes</mark>

{% swagger src="../../.gitbook/assets/openapi.yaml" path="/quotes" method="get" %}
[openapi.yaml](../../.gitbook/assets/openapi.yaml)
{% endswagger %}

#### Example:

```javascript
import fetch from 'cross-fetch';
import { parseEther } from 'ethers';

const baseUrl = 'https://test.orderbook.premia.finance'

// Free or Paid Tier API KEY
const MOCK_API_KEY = '3423ee2bfd89491f82b351404ea8c3b7'

// Params
const poolAddress='0xb9e594644D3BB24cfcBa3FA0289F18dB7cf81573'
const size= parseEther('5').toString()
const side='bid'
const chainId='421613'


async getQuotes(_addr, _size, _side, _chainId){
  const url = `${baseUrl}/quotes?poolAddress=${_addr}&size=${_size}&side=${_side}&chainId=${_chainId}`
	
  const response = await fetch(url, {
    headers: {
      'Content-Type': 'application/json',
      'x-apikey': MOCK_API_KEY
    }
  })
	
  if (!response.ok) {
    console.error('Request failed: ', await response.json())
    throw new Error(`Failed to fetch quote: ${response.statusText}`)
  }
	
  const quotes = await response.json()	
  
  return quotes
}

getQuotes(poolAddress, size, side, chainId)
```

### <mark style="color:blue;">Get rfq\_quotes</mark>

{% swagger src="../../.gitbook/assets/openapi.yaml" path="/rfq_quotes" method="get" %}
[openapi.yaml](../../.gitbook/assets/openapi.yaml)
{% endswagger %}

```javascript
import fetch from 'cross-fetch';
import { parseEther } from 'ethers';

const baseUrl = 'https://test.orderbook.premia.finance'

// Free or Paid Tier API KEY
const MOCK_API_KEY = '3423ee2bfd89491f82b351404ea8c3b7'

// Params
const poolAddress='0xb9e594644D3BB24cfcBa3FA0289F18dB7cf81573'.toLowerCase()
const side='bid'
const chainId='421613'
const takerAddress = '0xd18EE1c241e7A7e59797763C94d2Bd8C9169c831'


async getRfqQuotes(_addr, _side, _chainId, _taker){
  const url = `${baseUrl}/quotes?poolAddress=${_addr}&side=${_side}&chainId=${_chainId}&taker=${_taker}`
	
  const response = await fetch(url, {
    headers: {
      'Content-Type': 'application/json',
      'x-apikey': MOCK_API_KEY
    }
  })
	
  if (!response.ok) {
    console.error('Request failed: ', await response.json())
    throw new Error(`Failed to fetch quote: ${response.statusText}`)
  }
	
  const rfqQuotes = await response.json()	
  
  return rfqQuotes
}

getRfqQuotes(poolAddress, side, chainId, takerAddress)

```
