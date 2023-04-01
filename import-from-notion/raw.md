# Raw

A suite of upgradable smart contracts that together facilitates peer-to-peer market making and trading of options on ERC-20 tokens available on the Ethereum blockchain along with a settlement engine. This can be thought of as the “base” layer.

### Premia Vaults

A suite of in-house and third party smart contracts, composed on top of The Premia Protocol, that enables additional user functionality such as participation in automated strategies, leverage, and risk management on the Ethereum blockchain.

### Premia Interface

A web interface that allows for easy interaction with the Premia protocol. The interface is only one of many ways one may interact with the Premia protocol.

### Premia Governance

A governance system for governing the Premia Protocol, enabled by staking PREMIA token and receiving vePremia.

### Principles

One of the first principles of the Premia v3 protocol is to enable permissionless use by anyone in the world. This design decision was inspired by Ethereum's core ideals and our commitment to open access as a requirement for a future in which anyone in the world can access top financial services, no matter their life circumstances.

> Permissionless design means that the protocol's services are entirely open for public use, with no ability to selectively restrict who can or cannot use them. Anyone can swap, provide liquidity, or create new markets at will. This is a departure from traditional financial services, which typically restrict access based on geography, wealth status, and age. - Uniswap.org

### History

Premia is a peer-to-peer options exchange and settlement engine built for the Ethereum Virtual Machine (EVM). The protocol is designed to provide a set of smart contracts that advance open finance by prioritizing security, self-custody, automatic execution without a trusted intermediary, and permissionless use of financial primitives.

There are currently three versions of the Premia protocol:

* **Premia v1:** Peer-to-peer order-book based options exchange
  * Launched early 2021
  * Deprecated late 2021
* **Premia v2:** AMM-based options exchange
  * Launched late 2021
* **Premia v3:** Concentrated AMM-based options exchange w/ peer-to-peer order network
  * Launched early 2023

The protocol has advanced in functionality and efficiency with each new iteration. Previous versions will remain accessible with 100% uptime (even post-deprecation) via the Ethereum blockchain (though some features might not be maintained, such as the volatility surface for each token).

### Options on Premia

Premia options are [ERC-1155 tokens](broken-reference)(https://eips.ethereum.org/EIPS/eip-1155) that offer the holder the right (but not the obligation) to buy or sell the underlying token on a specified date. While traditional stock option contracts usually represent 100 shares of the underlying stock, options on Premia represent the same number of tokens as described.

_For example**,** a 100 ETH call option represents the right to buy 100 ETH at the option's strike price by the option's maturity date._

Each _option pool_ has a **token pair** (e.g. ETH/USDC), an **option type** (call or put), a **strike price** (the price at which the option can be exercised), and a **maturity date** (the expiration date of the option).

\<aside>

💡 Each option _is_ a pool and each market (ie. ETH/USDC) has multiple pools. Every option is defined by a token pair, expiration, type, and strike price.

\</aside>

Options on Premia v3 are _European_ in nature, meaning they can only be exercised at or after expiration. This is an update from Premia v2, in which options were American in nature, and could be exercised any time before or after expiration.

Call options use the Base (Underlying) Asset (ie. ETH for an ETH/USDC call option) for collateral where as puts use the Quote Asset (ie. USDC for an ETH/USDC put option). Each option is priced in the corresponding collateral asset.

The Premia Protocol (AKA the “base” layer) requires FULL collateralization. This means that for each _call option_ that is traded, the exchange must hold 1 unit of the Underlying Asset to ensure that there is no counter party risk. For each _put option_, the exchange must hold the Quote Asset equivalent to the strike price (eg. 1,800 USDC for a strike price of 1,800 ETH/USDC).

### Options Primer

**The largest use case for options is hedging risk** (i.e. buying insurance against) the downside risk of tokens one already holds via put options or on the upside risk of tokens one does not already own (or is short) via call options.

Options are also the most popular financial product to express views on volatility (and directional exposure). They exhibit many traits that allow users to curate their desired risk profiles by combining multiple options or using various expirations/strikes.

**Call options vs. Put options**

Call options provide the owner of the option the right, not an obligation, to purchase the described amount of underlying tokens at the specified strike price, by the option's maturity date. **Buyers of call options believe the underlying token **_**could**_** go up in price over time beyond the cost of the premium paid.**

\![Untitled](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/55e66186-301e-4961-9aa0-0cc1cb8b4844/Untitled.png)

Put options provide the owner of the option the right to sell the described amount of the underlying token at the described strike price, by the option's maturity date. **Buyers of put options believe the underlying token **_**could**_** go down in price over time time beyond the cost of the premium paid.**

\![Untitled](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e37064c-9af6-4b72-9643-174f7fa0adf2/Untitled.png)

*   **The Greeks**

    The specific risk metrics of each option can be measured in terms of 5 common variables, often called _The Greeks_. Traders often use these metrics to compare the risk profiles of different options and make decisions as to which option closer meets their strategy. It is important to keep in mind that The Greeks are dynamic, based on current market prices, and are constantly changing, meaning the variables are instantaneous in nature and should not be considered long-term truth values.

    *   **Delta**

        The change of option price due to price change of the underlying token. Call options have positive delta, put options have negative delta.

        \<aside>

        💡 _A Delta of 0.5 means the option price changes $0.50 for every $1.00 change in the price of the underlying token pair._

        \</aside>
    *   **Gamma**

        Rate of change of the option Delta given a change in price of the underlying token. Gamma is positive if you are long an option (call or put) and negative is you are short an option (call or put).

        \<aside>

        💡 _A Gamma of .01 means the Delta will go up(down) by .01 for every $1.00 change up(down) in the price of the underlying token pair._

        \</aside>
    *   **Theta**

        The change in option price caused by time value decay. Theta is positive if you are short an option (call or put) and negative is you are long an option (call or put).

        \<aside>

        💡 _A Theta of -5 means the option price will decay at a rate of $5 every day prior to expiration (all else being equal)._

        \</aside>
    *   **Vega**

        The change in option price caused by a change in an options implied volatility. Vega is positive if you are long an option (call or put) and negative is you are short an option (call or put).

        \<aside>

        💡 _A Vega of 2 means the option price will increase(decrease) by $2 for every 1% increase(decrease) in the option’s implied volatility._

        \</aside>
    * **Rho**

    The change in option price caused by a 1% change in an options interest rate (typicall the risk free rate). Calls have a positive Rho, Puts have a negative Rho.

    \<aside>

    💡 _A Rho of 0.5 means the option price will increase(decrease) $0.50 for every 1% increase(decrease) in the interest rate._

    \</aside>

### Order-book vs. AMM

Most traditional markets and centralized exchanges utilize central-limit order books (CLOBs) to track user orders and match overlapping trades. Traders familiar with traditional option brokers and crypto option exchanges will be familiar with order books, in which a depth of liquidity is maintained for each price level on the bid (buy-side) and ask (sell-side) of the market price by market **makers**, while **takers** can fill trades by accepting existing orders on the book.

In the Premia v3, market makers can deposit liquidity into **range orders** in an on-chain pool within the user’s defined price range (AKA concentrated liquidity). Makers can place range orders on the **buy-side,** **sell-side,** or **both**, to determine how their liquidity can be used within the specified price range. Each market’s automated price is directly determined by the distribution of liquidity on the exchange, and the past trades in the market. As traders (takers) buy options from sell-side orders, the market price will be adjusted upwards, and as traders sell options to buy-side orders, the market price will be adjusted downwards. This enables both traders and market makers to maintain short and / or long positions on the exchange as either makers or takers.

Each time a trade occurs, every overlapping range order will split fees and exposure for the trade pro-rata, determined by the amount of liquidity in each range order vs. the total amount of overlapping liquidity. The price each user pays or receives for an option is the quote price, determined by the AMM, plus a **taker fee.** The taker fee is split between makers and the protocol **stakeholders** (vePREMIA holders and protocol treasury).

Additionally, market makers can place limit orders on the v3 orderbook on Arbitrum Nova. These orders do not earn maker fees, however, they will still be quoted to users on the Premia Interface, if an order provides the best price for an option (subject to Small Order Flow optimization).

This duality enables Premia v3 users to benefit from both earning fees in automated range orders, as well as trade or market-make in traditional orderbook fashion. Traders on the exchange will additionally benefit from increased liquidity and better option pricing.

### Key Protocol Features

#### **Capital efficiency**

Liquidity providers are able to create concentrated range orders in an option pool with defined upper and lower price bounds. As traders move the market price through an LP’s price range, the LP will collect trading fees and the LP’s exposure will be updated. If the market price moves back down, the LP will collect more trading fees as the LP’s exposure will be reversed back to its original state.

A price range with more liquidity will require more option trades to be traversed than an equivalent price range with less liquidity, all else equal. This enables active traders with high conviction to benefit from highly capital efficient, concentrated orders, while passive traders with less conviction can still benefit from trading fees in a less capitally efficient range.

This increased capital efficiency can compounded by the use of a sell-side margin vault. The amount of collateral required to sell an option is often much larger than is required to buy the same option, thus causing an imbalance in option markets. A margin system introduced alongside the protocol enables sell-side LPs and option sellers (takers) to open positions on margin, up to an amount determined by an automated value-at-risk system.

#### **User functionality**

Traders, market-makers, and traditional LPs all receive additional functionality in this version of the protocol. Traders can buy or sell using market orders any time there is liquidity in the pool, with price impact determined by the size of the trade relative to the amount of liquidity in the effected price range(s).

LPs can place _uni-directional_ concentrated orders within a specific price range to express a position that will either get net-long or net-short as the market price traverses through the range.

Users with more passive intentions can utilize automated liquidity pools (vaults), built to manage specific trading, investment, and hedging strategies for the users within the vault’s liquidity pool.. The v3 system has been built as the base liquidity layer, on top of which many different strategies can be composed without liquidity fragmentation.

#### **Composability**

Diverse strategies can be created on top of the protocol, all benefiting from the more accurate price discovery, improved execution prices, and increased capital availability in the unified liquidity space. A wide range of vaults, traders, market-makers, and LPs can use the exchange for different reasons, without segregating and fragmenting liquidity for each use case. Due to the permissionless nature of the protocol, anyone can create a new market for an [ERC-20](broken-reference)(https://eips.ethereum.org/EIPS/eip-20) pair, so long as each token has an on-chain spot price oracle (data feed). Options on the protocol are represented as [ERC-1155 tokens](broken-reference)(https://eips.ethereum.org/EIPS/eip-1155) and LP positions are represented as [ERC-721 tokens](broken-reference)(https://eips.ethereum.org/EIPS/eip-721), to preserve maximum composability.

For each trade in a pool, the exposure change and fee growth is distributed pro-rata across all liquidity overlapping the traded price range. Fees are accumulated separately and not compounded back into LP positions, enabling vaults to distribute fees according to their specific strategies. Pool capital can be borrowed for a fee with flash loans, increasing protocol and LP revenue generation. In addition, the historic pricing and volatility of options in each pool can be queried from the pool’s time-weighted average oracle, enabling deep integrations within other protocols.

#### **Protocol sustainability**

The Premia v3 protocol requires no maintenance.

Additionally, the governance of liquidity mining emissions is entirely on-chain with the introduction of the vePREMIA system. This upgrade incentivizes stakers and LPs to more actively participate in reward distribution decisions, ensuring the pools with the highest expected fee returns receive the highest subsidies. Expired option positions can also be settled by any user of the protocol. This feature is self-financed by withholding collateral for the cost of EVM transaction fees (gas), enabling the feature to be permanently supported without external funding.

#### Incentivization

The protocol currently incentivizes Vaults to provide liquidity to the Premia Protocol with PREMIA liquidity mining rewards. The result is more trading volume, as takers receive better execution prices and have more liquidity to counter-trade. It follows that higher volumes will result in higher returns from fee distributions for stakeholders of the protocol.

LPs are additionally incentivized to stake the PREMIA they receive from liquidity mining rewards for vePREMIA, to earn a higher portion of trading fees, pay less fees on any taker trades, and direct more rewards to the pairs in which they receive the highest fee return.

To complete the incentive circle, vePREMIA stakers are incentivized to direct rewards to the vaults and pools that generate the most volume and highest fee return, as it will result in the highest return from fee distributions. All of these incentivizes work together to increase net volume and available liquidity, improve price efficiency, and enable higher returns for users of the platform.

### Quick Start

#### Connecting to a Chain & Wallet

Connecting to the UI can be done via the following wallets. If you do not have a wallet yet, you can use [MetaMask](broken-reference)(https://metamask.io/download/):

\![Screenshot 2023-03-28 at 12.22.21 PM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f4318a1-101c-4a59-a5fc-d671fc5c850a/Screenshot_2023-03-28_at_12.22.21_PM.png)

Premia V3 is currently available solely on Arbitrum Mainnet, while the orderbook is available on Arbitrum Nova.

#### Selecting an Option

From the Trade tab, there is the option to view markets in either a Basic layout or an Orderbook layout. The Orderbook layout will provide more details beyond just price. Additionally, the underlying, option type (Call or Put), and trade direction are used to help narrow down the option pools.

\![Screenshot 2023-03-28 at 10.01.09 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/068ecd31-05d4-4eff-bbbf-aa7cd62a98bd/Screenshot_2023-03-28_at_10.01.09_AM.png)

*   Selecting an Option

    To receive quotes, a Strike, Expiration and Option Size (Trade Size) are required.

    \![Screenshot 2023-03-28 at 10.02.07 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c4c6dbaa-f2a0-4df6-80e4-6a103feea179/Screenshot_2023-03-28_at_10.02.07_AM.png)

    Quotes will populate for a given market once all market parameters have been selected. Multiple quotes may appear and the source of these quotes may be of different origin (ie. Vault, Orderbook, or Option Pool). Additionally, markets with different oracles (but the same Token Pair), will also appear.

    The quotes are arranged in order of best price. By selecting a quote, a confirmation window will pop up to proceed with executing a trade. You can then select your payment token and see potential profit and loss.

    \![Screenshot 2023-03-28 at 10.02.27 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/850bc0d6-de3c-4e1b-bd94-929b3f7019f6/Screenshot_2023-03-28_at_10.02.27_AM.png)

    \<aside>

    ⚠️ It is prudent to note that trades can only be _closed_ using the market the trade was _opened_ in. For example, WETH/USDC (Chainlink) and WETH/USDC (Uniswap) are not the same market!

    \</aside>

#### Trading

*   Executing a trade (Basic)

    Prior to execution of a trade, basic information is given about the trade. Trades can be initialized with _any_ asset as collateral, but will be converted to the collateral asset of the option prior to executing the trade using a DEX aggregator. Users can set slippage controls for swaps if needed. The default is 0.5% slippage for swaps.

    \![Screenshot 2023-03-28 at 10.03.01 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d5245a35-91a6-4430-b1cd-c7c9935b8136/Screenshot_2023-03-28_at_10.03.01_AM.png)
*   Executing a trade (Orderbook)

    Using the Orderbook view for execution, we can see and traverse through multiple Expirations horizontally and Strikes vertically. Additionally, each Strike can be expanded to see additional information about the option itself, such as Implied Volatility, Bid/Ask Price & Size, Market Price, and Option Greeks.

    \![Screenshot 2023-03-28 at 10.05.02 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7045ed0d-8382-416e-a1d3-e31a3606478f/Screenshot_2023-03-28_at_10.05.02_AM.png)
*   Submitting a range order

    By selecting the Pools tab, we are able to begin the process of submitting a range order and becoming an LP (Liquidity Provider) for a specifc pool. Similar to executing a trade, details of the desired pool must be provided first.

    \<aside>

    💡 It is important to know that a single options market (Pair, Strike, Expiration, Type) makes up a single option pool. Therefore range orders are _option specific_. This is not to be confused with being an LP for a vault, which may trade many different options.

    \</aside>

    \![Screenshot 2023-03-30 at 10.46.46 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5bf1c87a-638c-49ea-bb28-a7cf07054731/Screenshot_2023-03-30_at_10.46.46_AM.png)

    \![Screenshot 2023-03-30 at 10.48.59 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0aafca10-030c-41c5-b267-1607ef9942b3/Screenshot_2023-03-30_at_10.48.59_AM.png)

    *   What does a Buy or Sell Range Order mean?

        Range orders are _side specific_. When initializing a range order, an LP must define the exposure type they would prefer. For example, if an LP would not mind a short exposure (or is depositing long option contracts they would not mind selling), the order time would be a SELL range order. Conversely, if an LP would not mind a long exposure (or is depositing short option contracts they would not mind closing), the oder time would be a BUY range orders.
    *   Min & Max Values of a Range Order

        Besides the size of the range order, a min and max price limit must be set. For convenience, an Auto-convert toggle is available to see prices in the quote asset.

        \![Screenshot_2023-03-28_at_14.20.10.png_](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d1e0e05-f0a5-4522-bd8c-5b107883e74a/Screenshot_2023-03-28_at_14.20.10.png)_

    For more information regarding Range Orders and how they work please see LP Range Orders.

#### Managing Positions

When a wallet is connected, a user is able to click on the Positions tab to see existing option positions for the given wallet address. If a user would like to close a position, it is best to select the option from your portfolio and close/modify the trade from here. By doing so, the position will be closed, and collateral released (if short).

Alternatively, positions can be closed directly from the Trade page. If the trade size is larger than the existing position, the position will first be closed before creating new exposure in the opposite direction.

\<aside>

💡 If using the Trade page to close a position, be sure that the oracle for the underlying market is the same, otherwise they are treated as two seperate markets.

\</aside>

\![Screenshot 2023-03-28 at 10.07.04 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3eccbca1-1865-4608-8ad8-75cb801d1e3b/Screenshot_2023-03-28_at_10.07.04_AM.png)

#### Staking Premia Token

Users may stake the Premia token for many reasons. In order to stake Premia tokens, a lock up period must be selected (zero days can be selected). The longer the lock period, the more influence (votes) the staked premia will have and the more staking rewards that can be earned. Staked Premia also shares in earnings from trading fees. Currently, any tokens not paid directly to LP’s are split 50/50 between stakers and the protocol.

For additional details on Governance and Voting, please see here.

\![Screenshot 2023-03-28 at 10.47.05 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/721fa0a6-7410-468e-a9f6-9fae9c581f36/Screenshot_2023-03-28_at_10.47.05_AM.png)

\![Screenshot 2023-03-28 at 10.46.48 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b837bf37-8382-4f0c-823c-e93c083c566e/Screenshot_2023-03-28_at_10.46.48_AM.png)

*   Voting

    Staked Premia allows a user to vote on liquidity mining emissions by Vault or Pool. There is incentive to direct liquidity mining emissions to active markets which generate the highest amount of fees, as it will generate higher USDC returns for stakers. Voting can be done at any time, and weights are updated on each block.

    \![Screenshot 2023-03-28 at 10.47.18 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f793929-654b-4987-ac51-72dd5b06a7fc/Screenshot_2023-03-28_at_10.47.18_AM.png)

    \![Screenshot 2023-03-28 at 10.47.50 AM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d8e9a6d5-e844-4c5f-a8b9-29c1f874f6dc/Screenshot_2023-03-28_at_10.47.50_AM.png)

#### Vaults

Vaults can be accessed through the Vault tab. Here you will find various single purpose vaults that allow participants to passively earn a return on their investment, manage risk, or hedge specific positions.

\<aside>

💡 Each vault has their own mandates and risk profiles. Please ensure that the risks and investment type are suitable for your needs. Additional information about vaults on this page can be found here.

\</aside>

\![Screenshot_2023-03-28_at_12.53.25.png_](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/166ae39b-2034-4127-8445-9afcbf8cad91/Screenshot_2023-03-28_at_12.53.25.png)_

After determining the appropriate vault, it is as simple as selecting the token that will be used for depositing (a swap will be performed if the asset is not the Vault asset).

*   Vaults Detailed

    Each vault has a detailed page in which specifications about the vault can be found

    \![Screenshot 2023-03-28 at 4.26.26 PM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c4f122c5-e8b0-4f5f-b7ca-d395214407ea/Screenshot_2023-03-28_at_4.26.26_PM.png)

### LP Range Orders

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

### Trading

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

### Fees

#### Trading Fees

Transaction fees are paid by traders taking liquidity (takers) and split between LPs (makers) and protocol stakeholders at a rate determined by governance. To retain higher composability, transaction fees are accumulated separately and not compounded back into LP positions.

The trading fee is calculated as follows:

\$$

Trading:Fee = max(0.03_Total:Premium,: 0.003_Size)

\$$

\$$

Total:Premium = Option:Price _Size_

\$$

\<aside>

💡 NOTE: Trading Fees are claimable at _any_ time by calling the `claim` function on the `IPool` interface.

\</aside>

#### Pool Initialization Fee

Pool creation is _permissionless **and fee based. The fee is dynamic and incentivizes users to initialize pools that are ATM and near-dated, as they are the cheapest to create. Additionally, discounts are provided for specific expirations and/or strikes that have not been initialized that would create spread trading opportunities. The formal math behind how this is determined can be found in Appendix A.2 of the**_ [_**Premia v3 whitepaper**_](broken-reference)_**(https://premia.finance/v3.pdf).**_

The fee for a pool initialization can be queried from the `IPoolFactory` interface using the initializationFee method. As a basic example, if a user wanted to initialize a 50 Delta option with 14 days to expiration, the fee to do so would be $25.

*   NOTE: Permissionless Pool Creation Bounds

    In order to prevent excessive fragmentation and ensure maximum composability with other option markets, pools can only be created for common strikes and expirations.

    Strikes are algorithmically limited to common values (log-rounded). The formal math behind how this is determined can be found in Append A.1 of the [Premia v3 whitepaper](broken-reference)(https://premia.finance/v3.pdf).

    The maximum expiration an option can be created with is 365 days out. Options will all expire at 8AM UTC, with all options over 7 days to maturity expiring on a Friday. All options past 30 days must expire on the last Friday of the month.

    Additionally, a spot market needs a valid oracle feed for the token pair (ie. ETH/USDC). Premia v3 has out-of-the-box support for any Chainlink oracle, Uniswap v3 pair, or custom oracle solution that implements the `IOracleAdapter` interface.

### Exercise & Settlement

When a user is long (or short) an option, they **can `exercise` (or** `settle`**)** their option from the `IPool` interface **at any time after the option’s maturity date**. If at the time of maturity, an option is [_In The Money_](broken-reference)_(https://www.investopedia.com/ask/answers/042715/what-difference-between-money-and-out-money.asp)_, **the payoff is locked to the intrinsic value and can be claimed at any time post-maturity by the owner of the long option. Short option holders can also claim the remaining value of collateral any time after expiration.** There is no penalty for late exercising or settlement.

\<aside>

💡 **Expired options can be exercised or settled by any approved user after expiration, if enabled by the option holder. The address settling the option will be compensated in return for the gas spent on settlement, up to the maximum fee set by the option holder in advance, in order to maintain self-sustaining auto-settlement.**

\</aside>

*   **Exercise/Settlement of a PUT option**

    If at the time of maturity, the price of the underlying asset is lower than the breakeven price, a put option is considered **In The Money**. In this case, the option owner (long the option) is entitled to the payoff, which is equal to the strike price of the underlying minus the spot price. This difference is calculated automatically and settled **in cash** (the quote token) to the option buyer. The option underwriter (short the option) is charged against their collateral held.

    **Example:**

    An user buys a 2 ETH/USDC put option, at a strike price of 3,000 USDC. At the time of exercise, the ETH price is 2,700 USDC. The user receives the difference between the strike price and the spot price (3,000 - 2,700), multiplied by the amount of options they own (2). In this case, the user receives 600 USDC on exercise. The counter party who is short the option must settle their position. They will 2,700 USDC for each option they were short (in which they provided 3,000 USDC as collateral).
*   **Exercise/Settlement of a CALL option**

    If at the time of maturity, the price of the underlying asset is higher than the breakeven price, a call option is considered **In The Money**. In this case, the user is entitled to the payoff, which is equal to the strike price of the underlying minus the spot price. This difference is calculated automatically and settled **in the underlying asset** (the base token) to the option buyer.

    **Example:**

    A user buys a 2 ETH/USDC call option, at a strike price of 3,500 USDC. At the time of exercise, the ETH price is 4,000 USDC. User receives the difference between the strike price and the spot price (4,000 - 3,500), multiplied by the amount of options they own (2). In this case, the user is entitled to 1,000 USDC, which is settled in ETH. Thus the user receives (1,000 / 4,000 ETH) = 0.25 ETH on exercise.
*   Settlement Price (Oracle Feed)

    Determining the settlement price is done via spot price oracles. In order to find out how the spot price is determined, please see here.

### Liquidity Mining

#### Vault Allocation

#### Future Pool Allocation

* Distribution over Volatility Surface

### Vaults

*   Overview

    Premia Vaults were originally named “Meta-Vaults”, because they were designed as passive liquidity Vaults that would enable users to take advantage of the current meta for options. In competitive gaming (not too far from the PvP nature of financial markets), meta or “metagame” is a term used to refer to the top tactics and strategies at the time, used by players to optimize for a specific environment or ruleset. Similarly, Premia Vaults are meant to be used by traders and yield seekers alike, to maximize their returns and risk-management success in DeFi.
*   Premia v3 Vaults

    The Margin Pool is a Premia Vault created in-house, intended to provide leverage to sell-side options on The Premia Protocol. This Vault will go live immediately after the launch of the V3 protocol, enabling lenders to earn interest relative to their risk, and option sellers to maintain lower capital requirements for their positions.

    In addition, there are other Vaults planned and being developed to go live in the near future. This includes the well-known C-Level Vault (Premia V2 Sell-Side Pools) and Knox Vaults, brought forward from the previous version of our platform by popular demand. These Vaults implement option selling strategies, to attempt to earn passive income. We look forward to adding additional composable Vaults to the platform, including Market-Making implementations in the future.
*   3rd Party Vaults

    Vaults can be created permissionlessly by anyone, to deploy strategies utilizing the Premia Protocol. Over time, we will be implementing a Contributor program, for showcasing Third-party Vaults on the Premia Interface, enabling Premia to benefit from increased volume and vault creators to benefit from performance fees. [Reach out](broken-reference)(https://www.notion.so/c5d64b5a68a94d2490e16040ade6dc1c) to build with us!

### Margin

#### Overview

Margin in of itself is a type of vault. It is built _on top_ of the base layer. This segregation from the base layer insures solvency and ability to guarantee payout as a settlement engine. Users who choose to utilize margin must do so through the margin vault. This experience is simplified for users of the Premia Interface or Premia v3 SDK. One of the major differences between using margin and using the base layer is that positions held by users on the base layer can be withdrawn and freely moved. Conversely, positions that utilize margin are not withdrawable.

The margin vault contains a blend of attributes from traditional Reg-T and Portfolio Margin systems that provide _sell-side_ leverage. A risk-based model is used to assess user positions in an isolated fashion (per-position). In order for the base layer to always remain solvent, margin users must borrow capital from pool lenders, which is then used to _fully collateralize_ the exposure on the base layer.

Borrowers are in “first-loss” position relative to the lender. This means all losses incurred on a position are debited from a borrow before the lender takes on any risk. All profit is retained by the user borrowing capital, less capital usage fees (interest).

#### Providing Liquidity as a Lender

Lending markets are established exclusively for the purpose of providing capital to option underwriters, where each collateral type (eg. ETH, WBTC, USDC) has its own margin lending pool.

When depositing capital into a margin pool, each lender must select a deadline on which their capital is to be returned. A lender's capital can be borrowed at any time before the deadline (or indefinitely if no deadline is set). For example, if a lender's deadline is 30 days from now, this implies the lender's capital will be available for up to the next 30 days, and will only be used for options that expire between the current time and the deadline.

Any lender capital utilized in an option position is locked for up to the expiration of the position. Upon borrowing, a borrower pays an upfront interest-based commitment fee based on the utilization of the total available capital in the pool, up to the option's expiration. When a borrower successfully closes a position, each lender's capital is unlocked and immediately made available for further lending or withdrawal. At any time, lenders may withdraw any of their capital that is not being utilized in the pool.

A lender's capital may be utilized for multiple options, so long as each expiration date is prior to the lender's deadline. All lenders for a specific expiration share in lending fees pro-rata. Additionally, lenders split principal risk of liquidated option positions, if and only if the Reserve Fund (discussed below) cannot fully cover losses. When a lender's deadline is passed, their capital will be reserved for withdrawal and will no longer be available to be borrowed for margin.

If a borrower closes a position before maturity, they will be rebated with commitment fee claim tokens, enabling the user to claim any potential commitment fees generated by the returned capital, if borrowed again by another user prior to maturity.

#### Selling on Margin

*   Lending Fee

    In order to sell on margin, a user must borrow funds so that the position is fully collateralized. Borrowing these funds requires paying interest. Interest is payed _up-front when a trade is opened._ Any interest left over (ie. a position is closed before expiration) is credited back to the trader upon closing the trade in the form or rebate claim tokens, which do **not** affect lender returns. The lending fee sits between the prevailing risk-free rate, `R` and `R + .05`. The amount of reserves relative to the amount of margined open interest determines where the interest rate will be. In other words, the more risk the lenders are potentially exposed to, the higher the interest rate charged up to 5% over the risk-free rate.

    For example, if there is 100 ETH in the ETH Reserve Fund, the first 100 short option positions opened on margin will borrow at the risk free rate. This is because there is no risk of loss to the lenders as any loss will be covered by the reserve fund. As the risk of loss to lenders becomes non-zero (the reserve fund capital becomes exposed), the interest rate will traverse to 10% to cover the risk of potential loss of their funds (as risk is transferred to lenders).

    \![Screenshot 2023-03-28 at 3.59.28 PM.png](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ed91bf73-4f8c-4457-8f33-9eeea1054d02/Screenshot_2023-03-28_at_3.59.28_PM.png)
*   Min Margin

    Minimum Margin is the least amount of collateral a position needs to maintain before it will be liquidated. It is important to know that this is a _dynamic_ number and will change over the life of a margined position based of several factors.

    *   Dynamics of Min Margin

        Time → As a function of time (all else equal), the Min Margin will _decrease_ as an option gets closer to expiration.

        IV → As a function of IV (all else equal), the Min Margin will _increase_ when an option’s IV increases.

        Price → As a function of price (all else equal), the Min Margin will _increase_ when an option’s price increases.

    \<aside>

    ⚠️ Under volatile market conditions, it is possible for margin to become temporarily unavailable for a given market (or option). If this were to happen, all positions that were opened using margin must be fully collateralized by users (or closed); otherwise positions will be liquidated. More technical details on the calculation method can be found in the [whitepaper](broken-reference)(https://premia.finance/v3.pdf) under section _6 Margin_.

    \</aside>

    At all times a user can monitor the Minimum Margin requirement for a given position and in the future, users will be able to set alerts directly on the Premia Interface to avoid liquidation.
*   Initial Margin

    Initial Margin is the minimum amount of collateral that must be provided by a user in order to open a _new_ short option position using margin. It is set to 1.5x the Min Margin. This ensures users have a substantial risk buffer before a position can be liquidated, once it is opened.

#### Liquidation

Liquidations do not instantly occur automatically on-chain. One of the of the major challenges with on-chain liquidation is price distortion, which is a function of liquidity. The less liquidity there is in a given market, the more it will be impacted by a liquidation event creating negative feedback loops. To solve for this, we’ve implemented a Reserve Fund structure (discussed next), which will help prevent negative feedback loops and can offset risk exposures for lenders as it grows.

*   Liquidation Trigger

    Anyone can liquidate an at-risk position on-chain and collect a liquidation fee for doing so. The liquidator does _not_ take on position exposure. They merely act as a keeper, monitoring for positions that can be liquidated, and invoking the `liquidate_position` function for LP exposures and `liquidate_trade` for taker positions.
*   Liquidation Fee

    The fee that is rewards to a liquidator is 0.3% of the total position value (capped at $10k USDC equivalent).
*   Liquidated Positions

    Liquidation events merely transfer ownership from the trader to the reserve fund. The position is then held by the reserve fund until expiration. _Traders who are liquidated lose their collateral (Minimum Margin) upon liquidation. Funds forfeited by the trader are then used to offset any potential loss._

    \<aside>

    💡 _Any additional funds left after expiration are allocated to the reserve fund to cover future potential losses._

    \</aside>
*   Determining Market Value

    Liquidations are determined based on an IV oracle which seeks to establish the fair market value of an option at any given point. This means that liquidations are not effected by pool prices. This has the added benefit of not triggering erroneous liquidations due to price wicks on the exchange. For further details on the IV Oracle, please see here.

#### Reserve Fund

Collateral in the Reserve Fund is meant to absorb the profit-or-loss of liquidated positions. Since lenders only provide capital to option positions that have times to maturity less than their deadline, the margin system is able to settle positions and abstract profit-or-loss variance from lenders before they are able to request a withdraw. _Simply stated, the Reserve Fund is in a first-loss position against lenders' principle._ Additionally, it is capable of distributing excess reserves as supplementary yield to lenders, akin to dividend payouts. If the Reserve Fund were to ever be insolvent, lenders' principle _could_ be exposed pro-rata to loss on liquidated positions.

\<aside>

💡 Keep in mind, as the Reserve Fund’s available capital decreases, the interest rate provided to lenders (required to borrow additional capital) may increase (if not already at the ceiling rate) to compensate for additional potential risk.

\</aside>

In the event that reserve funds can not completely cover all (potential) losses, they are utilized in order of option expiration first. For options that have the same expiration, options are settled with reserve assets on a _first-come, first-settle basis_.

### Oracles

#### Price Feed Oracles

*   Price Feed Overview

    In order to create an options market for a given token pair, a valid oracle must be available to determine the value of an option (based on spot price) at expiration. Premia v3 pools can be established out-of-the-box with Chainlink VWAP Price feeds or Uniswap v3 TWAP Price feeds. Additionally, any Price Oracle implementing the `IOracleAdapter` interface can be used to initialize a new option pool.

    By default, options will be automatically settled by an address maintained by the protocol, but Option holders can at any time designate an `autoSettleAddress` and an `autoMaxSettleFee`. Once set, the `autoSettleAddress` can exercise or settle options for the user after expiration, and be given a credit to compensate for the gas fees associated with making the call.

    For convenience a keeper bot is then used to hydrate each pool with its corresponding settlement price if the option has expired. However, this value can also be populated within each pool by _any_ user who calls the `exercise` or `settle` functions.
*   Chainlink

    Chainlink has many available feeds which can be found [here](broken-reference)(https://docs.chain.link/data-feeds/price-feeds/addresses?network=arbitrum). If a direct pair is not available when a pair is upserted to the `ChainlinkAdapter`, an attempt will be made to combine multiple price paths to create a valid price feed.

    To _initialize_ a pool, Chainlink is queried with the selected pair, and if a valid market exists, a VWAP price is returned to help determine the `initializationFee`.

    *   Determining Settlement Price

        Ideally, the settlement price of _any_ option would be determined by the spot price that corresponds exactly to 8AM UTC. If a price is _not available_ at this timestamp, there are several actions that are taken to determine the most appropriate price:

        1. A valid price _nearest_ to 8AM UTC on the expiration date is queried. This may end up being _before_ 8AM UTC or _after_ 8AM UTC, whichever is closest.
        2. If the last valid price is more than 25 hrs _before_ the expiration timestamp, it will revert. This will happen for up to 12 hrs _after_ the expiration timestamp.
        3. If expiration has happened more than 12 hrs ago, the last price prior to the expiration is used regardless of the timestamp (it will be more than 25 hrs prior to expiration).

        \<aside>

        💡 While it is not expected to be a common occurance to delay settlement by up to 12 hours, price feed or liquidity issues can happen.

        \</aside>
*   Uniswap v3

    Uniswap v3 pools can act like a time-weighted average price (TWAP) oracle for a given pair. This opens up the possibility for additional spot markets that may not be feasible with Chainlink oracles alone.

    \<aside>

    💡 Caution must be taken by users who choose to trade markets with Uniswap v3 TWAPS as there are [limited guardrails](broken-reference)(https://blog.uniswap.org/uniswap-v3-oracles) to prevent market price manipulation in Uniswap pools for less liquidity spot markets.

    \</aside>

    To _initialize_ an option pool using the `IUniswapV3Adapter`, Uniswap is queried with the selected pair, and if a valid market exists, a 10-minute TWAP is returned to help determine the `initializationFee` that can be queried ahead of time in the `IPoolFactory` interface.

    A time-weighted average price is provided through two functions, `quote` and `quoteFrom`, the TWAP period is by default 10 minutes. `quote` provides the TWAP using the latest observation. An observation is a recording of the pool state at a given block, it is updated after a swap is performed, if an observation for the current block has not been made. All pools must meet the required cardinality. This simply means that there must be enough observations to calculate a TWAP over a 10 minute period. `quoteFrom` adds an additional parameter, `target`. The `target` is the starting point from which the TWAP is calculated. For example, a target of 8:00AM UTC and a TWAP period of 10 minutes means that the TWAP is calculated from 7:50AM UTC to 8:00AM UTC.

    The price for both functions is derived from aggregating the arithmetic mean tick and harmonic mean liquidity across active fee tiers, then calculate a weighted arithmetic mean tick. To learn more detailsabout how Uniswap Price Oracles work, the [Uniswap v3 Handbook](broken-reference)(https://uniswapv3book.com/docs/milestone_5/price-oracle/) is a great place to start._

    \<aside>

    💡 It is also worth noting that Premia v3 option markets utilizing the `UniswapAdapter` require a Uniswap v3 pool on Arbitrum, since Arbitrum is the location of all option settlement for the protocol.

    \</aside>

    *   Determining Settlement Price

        Premia v3 will utilize a 10 minute TWAP window to determine prices that originate from Uniwap v3. For options that expire at 8AM UTC, we will use the TWAP from 750AM UTC to 800AM UTC on the corresponding expiration date.

        If a TWAP is _not available_ for this timestamp range, there are a couple actions that are taken to determine the most appropriate price:

        1. A valid price _prior_ to 750AM UTC is returned by Uniswap.
        2. If the oldest observation available is _after_ expiration, we will set the 10 min TWAP using the oldest observation.
*   3rd Party Oracles

    Any price feed that implements the `IOracleAdapter` smart contract interface can be used to initialize a new pool. However, only well-established price feeds will be shown directly to users on the Premia Interface or using the Premia v3 SDK.

#### IV Oracle

Notes:

Pending a change to amberdata instead of Deribit

* ESSVI → model derived from Deribit data (subject to change)
* Used for → Underwriter Vault & Margin Vault
* Updates → every minute

### Referrals

Referrals serve as a way for users to earn additional revenue and decrease their own trading fees on the protocol, by attracting volume and revenue to the protocol.

NOTES:

* url with wallet address design
* [vxref.me](broken-reference)(http://vxref.me) → takes premia domain and appends wallet
* Don’t have a portion breakdown of fees yet
* Just need to use it once and the referral address is permanent
  * First address a use gets referred by is permanent
* UI for this still pending

### Advanced Exchange Concepts

#### Orderbook & Request-for-Quote (RFQ)

Market makers can provide quotes to users off-chain, either on their own platforms or through quote aggregators like the Premia Orderbook API. This enables makers to provide quotes to traders, without having to spend EVM gas fees updating on-chain range orders. These orders do **not** earn maker rebates, ensuring concentrated liquidity stays competitive long-term.

#### Token Integration Requirements

#### Flash Swaps and Loans

### Overview

Users can participate in Premia Governance by staking (depositing & locking) their PREMIA tokens. In return, users will receive non-transferrable vePREMIA tokens, enabling them to share in fees generated by the protocol and participate in voting to distribute liquidity mining rewards to token pairs on the protocol.

### VePREMIA Staking & Voting — On-Chain

### Snapshot Voting — Off-Chain

### Process

### Beginners Guide to Voting

### Adversarial Circumstances

### V3 Changelog

### Whitepaper

Last Updated: Mar 24th, 2023

[Premia v3.pdf](broken-reference)(https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73e06730-fe23-462b-a284-4ed8dad30122/Premia_v3.pdf)_

### Calculations

See Whitepaper Appendix

### Media Kit

### Bug Bounty

### Audits

### Community Groups
