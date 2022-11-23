---
description: >-
  We have enlisted the brightest minds in DeFi to optimally solve the Volatility
  Surface problem on ETH mainnet.
---

# Volatility Surface Research

Intuitively, the approach we're taking is as follows:

1.  We start with an initial "best guess" for the volatility surface, with a limited input range (90 days to maturity and moneyness between 0.8 and 2.0, the most often traded strikes and maturities).

    **NOTE:** You can see that the large area in the center of the volatility surface is much more consistent and stable compared to the more erratic nature of the (less-traded) edges of the surface.
2. Any trade, weighted by magnitude, "pinches" the volatility surface in the direction of the trade. Intuitively, think of a bedsheet, which one can pinch and pull. The point pinched will have the most substantial effect, but areas around it will see this effect as well, depending on how far they are from the point of "pinch". The key design decision is to minimize the amount of trading needed to get from the initial best guess IVOL, to the theoretical market IVOL via continuous pinching.

**"Pinch" event selection**

If we observe a purchased option at some point on the volatility surface (for some maturity and strike price), we can infer that this transaction is causing upwards pressure on the surface localized at the point corresponding to the maturity and strike price of the option. However, the opposite pressures are not trivial to observe in a pool-to-peer architecture such as Premia.

For example, if an LP deposits funds in a pool, this deposit cannot be localized to a given part of the volatility surface (unless we ask the LPs to specify deposit params), but can just be attributed as a downwards shift of the volatility surface as a whole. The complete set of pinch events is still an open ended question, and something we're actively researching.

**Initial "best guess" surface**

The objective of the initial best guess surface is to minimize the total error from the theoretical market-clearing volatility surface. The key design decision is to approximate the order of magnitude of this error, s.t. the loss of efficiency faced by LPs can be offset by different incentive mechanisms. Intuitively, if we expect the initial surface to not differ by more than 10% from the theoretical surface, this means that the maximum discount that can be forced on the LPs will correspond to the % price decrease arising from 10% lower volatility input in the Black Scholes model.

Having a reasonable upper bound allows us to design incentive mechanisms such that both the LPs and the option buyers will get **at least fair value**.

**Some of the directions we've explored:**

* Inferring the dynamic IVOL surface from CeFi platform data (Deribit, Binance Options, etc.)
* Inferring the initial best guess surface from historical pricing data (static and dynamic replication models, monte carlo simulations, etc.)&#x20;
* Inferring signals from primary and secondary DeFi market transactions (e.g. Premia)

This research has lead us to create our own dynamic [Volatility Surface oracle](volatility-surface-oracle.md) to provide this final volatility data as a primitive to all of DeFi.&#x20;
