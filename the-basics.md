---
description: >-
  Premia is a decentralized options market based on a pool-to-peer architecture,
  similar to Uniswap or SushiSwap, but for options.
---

# The Basics

**Users can purchase American-style options** on Premia’s best-in-class AMM by first selecting the details of the option they'd like to trade, like the token pair, strike price, and maturity. Once the details have been entered, the user will receive a quote denoted in terms of the **underlying asset** for call options or the **base asset** for put options. If the user agrees with the price, they can execute the transaction to facilitate the trade and purchase the option for the quoted price.

![A user requests a price quote from the options pool](.gitbook/assets/flow.png)

**Users can purchase options with any asset** (so long as their is DEX liquidity available)**.** If users purchase an option with an asset other than the default payment token, the user's asset will be swapped to the payment token on the DEX with the best price before purchasing the option. This is done in a single transaction to ensure the best user experience.

All of the liquidity (capital) in the pools for trading options is provided by other users of the protocol called Liquidity Providers (LPs). When a trader purchases an option, another user, who has previously provided capital to the pool (an LP), simultaneously underwrites the option to the buyer. **All options on Premia are fully collateralized**, meaning the underwriters' tokens are locked in the option from purchase until settlement, to ensure the full exercise value of an option can always be paid out to option holders.

![Liquidity pools on Premia are user-managed and asset/direction specific.](<.gitbook/assets/4 (1).png>)

**Options on Premia can be exercised at any time before or after the option's expiration**. After an option's expiration, the option's value will be locked to the option's value at the time of expiration. When an option is exercised, the exercise reward is sent to the option holder and the remaining collateral is sent back to the LP's free capital pool, making it again available to be used again to underwrite future options or be withdrawn by the depositor (along with the premiums earned from selling the option).

Liquidity providers on Premia can take advantage of market-competitive yields from option premiums, in addition to Premia rewards from our Liquidity Mining program. This allows for traders to enjoy the best possible prices and trading experience, ensuring a consistent stream of volume and returns for LPs and PREMIA stakers.

