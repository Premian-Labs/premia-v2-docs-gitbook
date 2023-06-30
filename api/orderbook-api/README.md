# Orderbook API

### <mark style="color:blue;">Overview</mark>

The Premia Orderbook API can be used to _<mark style="color:green;">provide</mark>_ and/or _<mark style="color:green;">get</mark>_ quotes from the orderbook and RFQ system for any deployed/deployable option pool.   The Orderbook API comprises of both a [REST API](rest-api.md) and a [WEBSOCKET](websocket.md).

{% hint style="info" %}
Actions such as _cancelling_, _filling_, or _checking_ a quotes fillable status is done directly via the pool contract on Arbitrum One (see [pool contract](https://v3-docs.premia.finance/contracts/pool/IPoolTrade.sol/interface.IPoolTrade.html) for all available actions).  The reason for this is simply because the orderbook is merely a decentralized _broadcasting_ service for quotes. &#x20;
{% endhint %}

If desired, the API is also available through the [SDK](broken-reference)  via convenience wrapper functions.  It is not necessary to do direct calls to the API in order to use it. There is no centralized dependency to `Publish` or `Get` quotes.  The orderbook API is simply a convenience wrapper around web3 calls that can be made by anyone.&#x20;

### <mark style="color:blue;">Orderbook</mark>

As mentioned in the [Orderbook Concepts](../../concepts/advanced-exchange-concepts/orderbook-and-request-for-quote-rfq.md), quotes are published (by emitting events) to Arbitrum Nova and can be accessed by anyone listening to events on-chain. The Orderbook API will publish quotes for market makers _on their behalf_ and aggregate public order events to create an limit orderbook for any deployed/deployable pool.&#x20;

When posting an order, a `deadline` is provided in the quote object which specifies the duration a quote is valid for.  When a deadline is surpassed, the quote with expire without the need for action by the quote maker. However, if a user would like to prematurely void a quote before the deadline is hit, they must invoke the cancel function within the pool contract [here](https://v3-docs.premia.finance/contracts/pool/IPoolTrade.sol/interface.IPoolTrade.html#cancelquotesrfq).&#x20;

To _fill_ an order that was published to the orderbook, a user must call the fill function available on the pool contract [here](https://v3-docs.premia.finance/contracts/pool/IPoolTrade.sol/interface.IPoolTrade.html#fillquoterfq). Filling orders (as a taker) will incur a transaction fee.  Please see [Fees](../../concepts/fees.md) for more details.&#x20;

### <mark style="color:blue;">RFQ</mark>

Request-For-Quote is an additional feature available through the orderbook infrastructure in which users can publish _requests_ for a specific pool and receive _personalized_ quotes from market makers.

Publishing and receiving _requests_ are done via WEBSOCKET.  Makers subscribe to listen to RFQ requests and upon receiving the requests may _publish_ a quote.  _The requester is the only one who can fill the quote._

{% hint style="info" %}
The main difference between an RFQ quote and an orderbook quote is that the `takerAddress` is not populated for standard orderbook quotes.  They can be filled by any taker address on Arbitrum One, where as an RFQ quote can only be filled by the address populated in the `takerAddress` field.&#x20;
{% endhint %}
