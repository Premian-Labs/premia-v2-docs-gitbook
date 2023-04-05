# Options on Premia

Premia options are [ERC-1155 tokens](https://eips.ethereum.org/EIPS/eip-1155) that offer the holder the right (but not the obligation) to buy or sell the underlying token on a specified date. While traditional stock option contracts usually represent 100 shares of the underlying stock, options on Premia represent the same number of tokens as described.

_For example**,** a 100 ETH call option represents the right to buy 100 ETH at the option's strike price by the option's maturity date._

Each _option pool_ has a **token pair** (e.g. ETH/USDC), an **option type** (call or put), a **strike price** (the price at which the option can be exercised), and a **maturity date** (the expiration date of the option).

{% hint style="info" %}
Each option _is_ a pool and each market (ie. ETH/USDC) has multiple pools. Every option is defined by a token pair (oracle feed), expiration, type, and strike price.
{% endhint %}

Options on Premia v3 are _European_ in nature, meaning they can only be exercised at or after expiration. This is an update from Premia v2, in which options were American in nature, and could be exercised any time before or after expiration.

Call options use the Base (Underlying) Asset (ie. ETH for an ETH/USDC call option) for collateral where as puts use the Quote Asset (ie. USDC for an ETH/USDC put option). Each option is priced in the corresponding collateral asset.

The Premia Protocol (AKA the “base” layer) requires FULL collateralization. This means that for each _call option_ that is traded, the exchange must hold 1 unit of the Underlying Asset to ensure that there is no counter party risk. For each _put option_, the exchange must hold the Quote Asset equivalent to the strike price (eg. 1,800 USDC for a strike price of 1,800 ETH/USDC).
