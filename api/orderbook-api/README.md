# Orderbook API

### <mark style="color:blue;">Overview</mark>

The Premia Orderbook API can be used to  [Provide](publish-quote-s.md)  and/or [Get](get-quotes.md) quotes for any deployed option pool.  As mentioned in the [Orderbook Concepts](../../concepts/advanced-exchange-concepts/orderbook-and-request-for-quote-rfq.md), quotes are published (by emitting quote events) to Arbitrum Nova and can be accessed by anyone. The Orderbook API will publish quotes for market makers _on their behalf_ and aggregate order events to create an orderbook for any deployed pool.&#x20;

{% hint style="info" %}
It is important to note that there is no centralized dependency to Publish or Get quotes.  The orderbook API is simply a convenience wrapper around web3 calls that can be made by anyone.
{% endhint %}

If desired, the API is also available through the [SDK](broken-reference)  via convenience wrapper functions.  It is not necessary to do direct calls to the API in order to use it.&#x20;
