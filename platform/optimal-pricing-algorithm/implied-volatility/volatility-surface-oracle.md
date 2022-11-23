---
description: >-
  Premia has partnered with Chainlink to provide our Volatility Surface on-chain
  for all of DeFi.
---

# Volatility Surface Oracle

Based on our extensive background of research on options volatility, specifically in crypto markets, and inspired by the extreme lack of volatility tools in DeFi, we have decided to launch our own Volatility Surface oracle. Similar to existing Price Feed oracles (such as those used by Premia pools), our Volatility Surface oracle will allow any smart contract to query the data from on-chain, allowing external contracts to accurately price options or measure risk at a granular level using this volatility data.

Early on in our research, we realized it was extremely important to provide a full 3-dimensional volatility surface for pricing options. The term structure (how the volatility changes over time) and the volatility smile/skew (how the volatility changes in regards to option "moneyness") cannot be ignored, otherwise options will be wildly mis-priced. This, coupled with the low-compute constraints of the Ethereum mainnet, means we are forced to calculate the ideal volatility surface off-chain, and periodically report the updated surface to the on-chain oracle through the use of decentralized technology such as [Chainlink nodes](https://chain.link/ecosystem).

We use a volume-weighted combination of the most liquid CEX options data, along with data from trades executed on the Premia platform, to form our three-dimensional, off-chain volatility surface for each pool. This surface is then parameterized so it can be put on-chain as a simple polynomial, allowing for any area on the surface to be accurately priced.

To price an option, a user (or contract) can call `getBlackScholesPrice` on the Volatility Surface oracle contract, passing in the token pair, call or put, the spot price, the strike price, and the maturity of the option. This will return the Black Scholes price with the volatility surface value for that specific option plugged into the $$\sigma$$ value in the original $$BS$$ equation.

However, option pricing is not the only usage for volatility surface data. If one would like to get the entire surface, they can call `getVolatilitySurface` , passing in the token pair. Alternatively, one can call `getAnnualizedVolatility64x64,` with the same parameters as passed to `getBlackScholesPrice`, to get the 64x64 fixed decimal representation of the volatility for a specific option.

The pairs currently supported by the Premia Volatility Surface oracle:

**WETH/DAI** Call and Put - Market-based surface

**WBTC/DAI** Call and Put - Market-based surface

**LINK/DAI** Call and Put - Synthetic surface (no sufficiently liquid external option markets exist)

**We are excited to make this Volatility Surface data available for all of DeFi to build on-top of.**
