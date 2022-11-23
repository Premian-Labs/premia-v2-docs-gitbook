---
description: A few notes on American vs European option pricing.
---

# American Option Pricing

There exist several models that often do a better job of pricing American options than vanilla Black-Scholes. The Binomial Option Pricing Model (BOPM) is a good example. However, due to the computation costs on Ethereum mainnet, a BOPM implementation is not feasible.

There exist several variants of the Black Scholes models adjusted for American options pricing. Most of them, however, simply add an adjustment coefficient that takes the unobservable "probability of exercise" as an input value. In other words, the mapping from vanilla $$BS$$ to American-adjusted-$$BS$$ is usually done in the form of a coefficient that may or may not be stable across time and cannot be computed on-chain efficiently. In any case, given the nature of this relationship, there is no reason that the C-value should converge to a level that disregards this European-American adjustment.
