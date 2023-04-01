# Trading

###

#### Overview

Traders on the Premia v3 exchange (market takers) can receive a quote to buy (or sell) an option from (or to) LPs in an option pool at the quote price. If the taker accepts the quote, they can market buy (or sell) the option and pay (or receive) a premium in addition to receiving long (or short) option exposure, while also incurring a transaction fee.

In addition to quotes from option pools, traders may receive quotes from Vaults or the Orderbook API, which will be cleared and settled through the option pool for the specific option traded. Users of the Premia Interface or Premia v3 SDK will have easy access to the best quotes from each source.

The long (or short) option is then owned by the purchaser and represented as an [ERC-1155 token](broken-reference)(https://eips.ethereum.org/EIPS/eip-1155) in their wallet, allowing the user to transfer the option, trade, or exercise (or settle) it at a future time.

\<aside>

💡 The difference between a pool’s current `marketPrice` and `getTradeQuote` in the `IPool` interface is _price impact of a potenital trade_. This is a function of market liquidity and order size.

\</aside>

#### Executing a Trade

**Example:** Buying a call option

**1**. Send a request to the router for the pool, specifying the following values:

* **strike price**
* maturity
* option type
* size of option

_(example: ETH/USDC call option, with strike price 3,500 USDC; maturity 30 days; option size of 2 ETH)‌_

\<aside>

💡 _**Keep in mind these details are automatically sent to the correct Pool to retrieve a quote for the user when a specific option is selected on the Premia web interface.**_

\</aside>

**2.** Pool sends back a quoted price for the option.

**(e.g: 0.1 ETH)‌**

**3.** If the user agrees with the price, they can confirm and execute a transaction to purchase the option at the specified price (allowing for slippage, in case another user simultaneously purchases an option from the pool). If the user would like, they can purchase the option with any token in their wallet (e.g: 200 USDC), and the token will be automatically swapped at the optimized market-rate to the token required to purchase the option (e.g: 0.1 ETH).

**4.** When the transaction is confirmed, the user receives the European option they purchased. The user can then exercise the option at any time after expiration to unlock the rewarded tokens in the option and return the remaining capital to the pool. After expiration, if an option has not been exercised, its exercise value is locked to the value of the option at the time of exercise.

This ensures the option holder always receives the full value of their option and liquidity providers can immediately recover their capital after expiration.

\<aside>

💡 **Users can close previous trades by selling (or buying) the option back to (or from) the pool at the market price.**

\</aside>
