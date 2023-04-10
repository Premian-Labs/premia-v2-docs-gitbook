# Orderbook & Request-for-Quote (RFQ)

## <mark style="color:blue;">Arbitrum One vs. Arbitrum Nova</mark>

The Orderbook architecture is unique in that _two_ separate chains are utilized. The primary chain is [Arbitrum One](https://arbitrum.io/). Just like the v3 protocol, it's the primary chain where all orders are filled, cancelled, and positions settled/exercised.   RFQ functionality can be done using the `IPool` interface, which resides on Arbitrum One. Users of the Orderbook must have a valid address on Arbitrum One. All collateral and approvals to transfer collateral must be on Arbitrum One.&#x20;

Providing _quotes_ for the orderbook are done through [Arbitrum Nova](https://nova.arbitrum.io/).  Quotes are nothing more than emitted events of order details that are signed by the maker of the quote for a transaction that will process on Arbitrum One.   There are two primary ways to emit quotes to the orderbook:

1. Directly through the `IOrderbookStream` interface using `add`.  This contract resides on Arbitrum Nova and requires a maker to have an account with an ETH balance to pay for gas fees. &#x20;
2. Using the [Premia Orderbook API](../../api/orderbook-api.md),  Premia will publish the quote on Arbitrum Nova on the makers behalf.   This is a rate limited / tiered feature.

{% hint style="info" %}
These orders do **not** earn maker rebates or liquidity mining rewards, ensuring concentrated liquidity and vaults stay competitive long-term.
{% endhint %}
