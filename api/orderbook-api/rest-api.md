---
description: Overview
---

# REST API

### <mark style="color:blue;">Overview</mark>

| Chain                    | Base Url                              |
| ------------------------ | ------------------------------------- |
| Arbitrum Goerli (421613) | https://test.orderbook.premia.finance |
| Arbitrum One (42161)     | https://orderbook.premia.finance      |

Users can access the [`GET` Quotes ](broken-reference)and [`POST` Quotes](broken-reference) methods of the REST API _directly_ using the `/quotes` end-point.  In order to use REST API endpoints, you must also pass in an API KEY

### <mark style="color:blue;">Publish Quotes</mark>

{% swagger src="../../.gitbook/assets/openapi (1).yaml" path="/quotes" method="post" %}
[openapi (1).yaml](<../../.gitbook/assets/openapi (1).yaml>)
{% endswagger %}

#### Example:

```javascript
import fetch from 'cross-fetch';

const url = 'https://test.orderbook.premia.finance/quotes'

// Free or Paid Tier API KEY
const MOCK_API_KEY = '3423ee2bfd89491f82b351404ea8c3b7'

// object array of one or more quotes
const mockQuotes = [{
  poolKey: {
    base: '0x9f5D1212514Ac88E26c523387C60F87B67AD1130',
    quote: '0x53421DB1f41368E028A4239954feB5033C7B3729',
    oracleAdapter: '0xB89756634Bae979d13721d9883e67CF22cc31D6b',
    strike: '29000000000000000000000',
    maturity: 1688716800,
    isCallPool: false
  },
  chainId: '421613'
  provider: '0x9E600587b9035a8C1254E8256F4E588CC33B8467',
  taker: '0x0000000000000000000000000000000000000000',
  price: '195000000000000000',
  size: '1000000000000000000',
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

{% swagger src="../../.gitbook/assets/openapi (1).yaml" path="/quotes" method="get" %}
[openapi (1).yaml](<../../.gitbook/assets/openapi (1).yaml>)
{% endswagger %}

#### Example:

```javascript
import fetch from 'cross-fetch';
import { parseEther } from 'ethers';

const baseUrl = 'https://test.orderbook.premia.finance'

// Free or Paid Tier API KEY
const MOCK_API_KEY = '3423ee2bfd89491f82b351404ea8c3b7'

// Params
const poolAddress='0xb9e594644D3BB24cfcBa3FA0289F18dB7cf81573'.toLowerCase()
const size= parseEther('5').toString()
const side='bid'
const chainId='421613'


async getQuotes(_addr, size, side, chainId){
  const url = `${baseUrl}/quotes?poolAddress=${_addr}&size=${size}&side=${side}&chainId=${chainId}`
	
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
