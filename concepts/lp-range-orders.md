# LP Range Orders

#### Overview

Range orders are at the core of concentrated liquidity, they allow LPs to deposit over a specific price range defined by a _lower price bound_ and _upper price bound_. Orders that span the minimum price width can replicate limit orders similar to orders placed on a limit order-book (if only crossed a single time), while orders spanning across multiple price points (called _ticks_) replicate orders placed _linearly_ over multiple adjacent prices. There is no commitment period for LP deposits. They can be withdrawn prior to expiration.

Premia v3 uses an accounting method called Split-User Accounting. At the core, this accounting process allows LPs to define directional exposure of a range order. This is automatically determined based on the asset that is deposited (Collateral or Option Contracts) along with the orientation of the order relative to the current market price. Simply put, range orders provide _uni-directional_ exposure (either buy **or** sell). More information about how Split-User Accounting works can be found in Section 4 of the Premia v3 whitepaper here.

#### Range Order (Basics)

In order to define a range order, 3 primary inputs must be provided to the `deposit` function in the `IPool` interface:

* Lower Tick ⇒ lower price bound
* Upper Tick ⇒ upper price bound
* Size (liquidity) ⇒ Size of Collateral OR Option Contracts

\<aside>

💡 In order to find the pool address, users can query the `getPoolAddress` function in `IPoolFactory`.

\</aside>

When liquidity is deposited above the market price, this order can be initially viewed as _ask-side liquidity_. Similarly, deposits below the market price can be initially viewed as _bid-side liquidity_. As the market price moves up and down through a range, the liquidity provider collects maker fees, in addition to any exposure changes.

\![Screenshot 2023-03-23 at 11.52.39 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2b136a2-941e-4c5f-95a1-b4ad2c6afccc/Screenshot_2023-03-23_at_11.52.39_AM.png)

*   Depositing Collateral

    If an LP deposits collateral, they are suggesting that they would like to get _long_ option contracts if they are posting a bid-side range order and _short_ contracts if they are posting an ask-side range order. These range orders can be thought of as “buy-to-open” or “sell-to-open” order types initially. As the market price traverses through these range orders, they will become “sell-to-close” and “buy-to-close” range orders respectively.

    \<aside>

    💡 An ask-side range order with collateral can never be net _long_ options just as a bid-side order with collateral can never be _short_ options.

    \</aside>
*   Depositing Option Contracts

    If an LP deposits option contracts, they are suggesting that they would like to close their position_._ Bid-side orders can be made with short option contracts, and Ask-side orders can be made with long option contracts. These order types can be thought of as “buy-to-close” and “sell-to-close” order types initially. As markets traverse back and forth through these range orders, an LP may re-establish the original option exposure they deposited with.

    \<aside>

    💡 An ask-side range order with long options can never get net short options. A bid-side order with short options can never get net long options.

    \</aside>

#### Range Order (Detailed)

It is best to illustrate a detailed view of a range order through an example. Here, we will be focusing on a range order with the following details:

* Option type ⇒ Call Option
* Current Market Price ⇒ 0.35
* _Initial_ Range Order Type ⇒ _bid-side liquidity_
* Lower Tick ⇒ 0.25
* Upper Tick ⇒ 0.30
* Deposit ⇒ 1 Unit of Base (Underlying) Asset as collateral

As the price of the option moves _down_ (right to left), the collateral which was initially deposited (1 unit) begins to decrease (transferred to takers) as the market price enters and traverses through the order range. The collateral is used to purchase _long_ option contracts from traders.

Once this order is fully traversed (ie. market price is now 0.20), the range order consists of 3.63 options and 0 collateral. Note, any fees collected are not part of the collateral balance and are separately redeemable. At this point, the order is considered sell-side liquidity, which consists of Option Contracts that will be sold to collateral if the price of the option were to go up (left to right).

It is worth noting that pricing is linear, which means the average execution price of a range is simple `(Upper Tick + Lower Tick)/2`. In this example of a sell-side order, the average execution price is 0.275.

\![Screenshot 2023-03-23 at 12.15.57 PM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a80fb45a-630d-4692-96df-0a1e009719bf/Screenshot_2023-03-23_at_12.15.57_PM.png)

#### Range Order (Advanced)

In addition to the 3 core inputs of a range order (Lower Tick, Upper Tick, Size), users must also supply a `minMarketPrice` and `maxMarketPrice` when directly interacting with the `deposit` function. Market price here refers to the _option_ price.

By specifying a min/max marketPrice for the option, LPs can get granular control of the composition of asset(s) that are used for collateral. It can be thought of as slippage limitations.

*   Range Orders that straddle market price

    It is possible to initialize a range order that “straddles” the current market price. This would mean Lower _Tick < Market Price < Upper Tick_. In this case, a deposit will need to consist of BOTH options and collateral (linearly interpolated based on the core order inputs and market price).

    Setting the `minMarketPrice` and `maxMarketPrice` to a narrow range ensures the composition of the order is within tolerance.

For orders that are intended to be solely _bid-side_ or _ask-side_ liquidity with a SINGLE collateral type (options OR collateral), the minMarketPrice and maxMarketPrice are primarly helpful when an LP holds a mixture of options and collateral in their wallet, but strictly wants to use only one or the other. When placing a range order that is close to the market price, there is risk of an unintended straddle.

Unintended Straddle Example

An LP holds ETH and short options in their wallet. Their intention is to create a _bid-side_ range order to close the existing short exposure. The range is set just below the current market price (Upper Tick < Market Price). In the process of creating the range order, the market price moves down _into_ the LPs order range (thus creating an unintended straddle). The `Deposit` function would seek a small portion of the LPs ETH and leave behind a small portion of the short option contract in the users wallet.

Setting the `minMarketPrice` to the Upper Tick would cause the transaction to revert, allowing the LP to adjust the range order and resubmit. `maxMarketPrice` is trivial in this example, but still requires a value > market price.
