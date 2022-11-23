---
description: >-
  Every pool has a C-level (price level) at any given time. The higher the
  C-level, the more expensive the options, the higher the premiums earned on
  capital by LPs.
---

# C-level - Capital Pricing and Initial Liquidity

![](<../../../../.gitbook/assets/c level.png>)

### **TLDR;**

* **C-level is the unique Premia mechanic that regulates the option price levels in a pool, according to the relative supply and demand of capital in the pool.**
* **When the C-level is high, options are expensive and LPs earn a higher return on capital.**
* **As a LP you want to provide more liquidity when the C-level is high.**
* **Each pool is given a high C value on initialization - LPs can get in early for the highest likelihood of above market risk-adjusted returns.**

To best understand how the C-level works, let's consider a newly created ETH/DAI put pool. Let's suppose that the initial $$C_0$$ value with which the pool is initiated is $$C_0=5$$. **Intuitively, the C-level is the dynamic multiple to the base Black-Scholes model that adjusts after every trade.** This means that initial pool prices are set to $$5 * BlackScholesPrice$$.

At $$C_0=5$$, the options in that pool are almost guaranteed to be overpriced (by design) - this is good for LPs. As an LP, I want to provide liquidity to such a pool, in case some option buyers are either irrational or have an extremely high willingness to pay for ETH/DAI put options. But while $$C_0$$ is high, this is almost guaranteed to attract more LPs than buyers. \
\
**Note:** The pools are liquidity aware. Every time liquidity is added, the C-level decreases. Every time options are purchased (causing free liquidity to be removed), the C-level increases.&#x20;

![Price level will trend towards the market-clearing C-level and is resilient to high volatility.](../../../../.gitbook/assets/3.3.png)

As LPs continue to deposit capital into the new pool, they will drive down the pool price levels to a market clearing price range, after some number of transactions, _n_. If we assume that, after _n_ transactions, the pool converges to the market clearing C-value, $$C_{clearing}$$, the LPs will continue earning market-competitive returns on their liquidity.

However, before the C-level converges to $$C_{clearing}$$, there are very likely to be buyers willing to overpay for the options, thus generating early LPs above market risk-adjusted returns (for the capital that is utilized).

#### **Theoretical pool utilization will reach 100% at the limit**

Due to the design of Premia pricing mechanics, each pool will always converge towards a theoretical 100% utilization. For the LPs this is great, because none of their capital will be sitting idle. All the liquidity deposited by an LP will be incentivized to be utilized at the best market return. However, practically, there will always be deviations from 100% utilization for reasons such as buyers needing free liquidity, withdrawals, gradual divestment, etc. and the Liquidity Buffer.

The **Liquidity Buffer** is the excess liquidity available in the pool, created by the initial C-value convergence. In other words, between the pool being initialized and the C-level reaching $$C_{clearing}$$, not all of this capital will be utilized, since it's assumed to be overpriced. Simulations show that once $$C_{clearing}$$ is reached, the free capital in the pool will roughly hover around the liquidity buffer levels, though over time this buffer will become an increasingly smaller portion of the total pool size because the buffer is denoted in nominal terms, not percentage terms.

****
