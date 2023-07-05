---
description: Websocket Functionality
---

# WEBSOCKET

### <mark style="color:blue;">Overview</mark>

| Chain                    | Websocket Url                    |
| ------------------------ | -------------------------------- |
| Arbitrum Goerli (421613) | wss://test.quotes.premia.finance |
| Arbitrum One (42161)     | wss://quotes.premia.finance      |

Using the WEBSOCKET connection, it is possible to:

* [_<mark style="color:blue;"><mark style="color:green;">Stream<mark style="color:green;"></mark>_](websocket.md#subscribe-to-quotes-orderbook-and-rfq) public/RFQ quotes from the orderbook in realtime
* [_<mark style="color:green;">Publish</mark>_](websocket.md#publish-rfq-request-s) an RFQ requests (for market takers) to _receive personalized_ quotes
* [_<mark style="color:green;">Receive</mark>_](websocket.md#subscribe-to-rfq-requests) _RFQ_ requests (for market makers) to subsequently provide personalize quotes

### <mark style="color:blue;">Authorize Websocket</mark>

Upon connection with the Websocket server, users must send an `AUTH` message with an api key.  If this step is not done, any requests to _Stream_ quotes or _Publish_ RFQ requests will be denied.&#x20;

{% tabs %}
{% tab title="Authorization Example" %}
```javascript
const { WebSocket } = require('ws')
const wsUrl = 'test.quotes.premia.finance'
const MOCK_API_KEY = '3423ee2bfd89491f82b351404ea8c3b7'

function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms))
}

const authMessage = {
  type: "AUTH",
  apiKey: MOCK_API_KEY,
  body: null
}

/*
Optional params in body include:
poolAddress -> specific option market
size -> stringified 10^18 value
side -> 'bid' or 'ask'
taker -> taker address
provider -> quote provider address
 */
const filterMessage = {
  type: 'FILTER',
  channel: 'QUOTES',
  body: {
    chainId: '421613',
    poolAddress: '0xeB785e131784ea28b6B64B605CF8aa83D69793b5'
  }
}

const ws = new WebSocket(`wss://${wsUrl}`)
function connectWebsocket() {
  ws.onopen = (event) => {
    console.log("Websocket connection open")
    event.target.send(JSON.stringify(authMessage))
    event.target.onmessage = (event) => {
      console.log(JSON.parse(event.data).message)
    }
  }
}

connectWebsocket()
```


{% endtab %}
{% endtabs %}

### <mark style="color:blue;">Subscribe to Quotes (Orderbook & RFQ)</mark>

Subscribing to quotes allows a user to stream real time quotes that are published to the orderbook along with any private quotes that may also be available from an [RFQ request](websocket.md#publish-rfq-request-s).  By default, ALL public quotes are subscribed to upon authorization of a websocket connection. `FILTER` messages are required.



{% tabs %}
{% tab title="Subscribe Example" %}
```javascript
			
```
{% endtab %}
{% endtabs %}

### <mark style="color:blue;">Publish RFQ Request(s)</mark>

\<UNDER CONSTRUCTION>

### <mark style="color:blue;">Subscribe to RFQ Requests</mark>

\<UNDER CONSTRUCTION>
