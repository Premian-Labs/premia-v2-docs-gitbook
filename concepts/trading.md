# Trading

### <mark style="color:blue;">Overview</mark>

Long (short) options are represented as an [ERC-1155 token](https://eips.ethereum.org/EIPS/eip-1155) in a wallet. It allows any EOA or Contract address to easily transfer, trade, or exercise (settle) the option at a future time. When taking liquidity from any source, a transaction fee will need to be paid. More details on fees can be found [here](fees.md#trading-fees).

While all options settle within their respective pools, it’s possible to interact with _multiple_ sources of liquidity for the same option. Users of the [Premia Interface](../#the-premia-interface) or Premia v3 SDK will have easy access to the best quotes from each source. Please see here for more details about receiving a quote.

There could be up to 4 sources of liquidity for a given option:

1. AMM - Range Orders
2. Orderbook / RFQ System
3. Vaults
4. External Protocols / Third Parties

Interacting with the [AMM](trading.md#amm) and [Orderbook / RFQ](../the-premia-protocol/order-book-vs.-amm.md) System can be done directly via the `IPool` interface while [Vaults](vaults.md) and [External Protocols](trading.md#external-protocols-third-parties) would involve directly corresponding with their contracts or interfaces if not available on the Premia Interface or Premia v3 SDK.

### <mark style="color:blue;">AMM</mark>

Traders on the Premia v3 exchange - takers - can receive a quote to buy (sell) an option from LPs in an option pool at the given quote price using `getQuoteAMM`. If the taker deems the quote acceptable, they can `trade` the option and pay (receive) a premium in addition to receiving long (short) option contracts in the form of [ERC-1155 tokens](https://eips.ethereum.org/EIPS/eip-1155).

The trade function has 3 inputs: `size`, `isBuy`, and `premiumLimit`. The `size` parameter refers to the order size, `isBuy` is a boolean to signify trade direction, and `premiumLimit` is used for slippage control. If an order trades beyond the `premiumLimit`, ie. the average execution price of a buy (sell) order is above (below) the `premiumLimit`, the transaction will revert.

{% hint style="info" %}
The difference between a pool’s current `marketPrice` and `getQuoteAMM` in the `IPool` interface is the _price impact_ of a potential trade. This is a function of market liquidity and order size, where more a higher ratio of order size to existing liquidity will result in a higher price impact and vice versa.
{% endhint %}

It is possible to both pay and receive premiums and / or collateral for an option in the token of a user’s choice. This requires the user to define their swap parameters in the form of _calldata_, which will enable the swap to be executed on-chain before or after the necessary action to convert a token. The `swapAndTrade` and `tradeAndSwap` functions on each AMM pool can be used to facilitate this feature. More details can be found in the `IPool` interface within the Contract section.

### <mark style="color:blue;">Orderbook / RFQ System</mark>

### <mark style="color:blue;">Vaults</mark>

### <mark style="color:blue;">External Protocols / Third Parties</mark>
