---
description: >-
  Premia uses a hybrid cash settlement mechanism to minimize the amount of funds
  that need to change hands. All Premia options are fully collateralized at all
  times
---

# Exercising & Settlement

When a user buys an option, they **can exercise their option at any time after purchase**. Options can be exercised in full or in partial amounts over time. If at the time of maturity, an option is _In The Money_**,** the payoff is locked in and can be claimed at any time post maturity by the owner of the option. **There is no penalty for late exercising.**

**Exercising and settlement of a PUT option**

![Put options rise in value as the underlying tokens drops in value.](<../../.gitbook/assets/2.1 (1).png>)

If at the time of exercise, the price of the underlying asset is lower than the breakeven price, the put option is considered **In The Money**. In this case, the user is entitled to the payoff, which is equal to the strike price of the underlying minus the spot price. This difference is calculated automatically and settled **in cash** (the base token) to the option buyer.&#x20;

**Example:** A user buys a 2 ETH/DAI put option, at a strike price of 3,000 DAI. At the time of exercise, the ETH price is 2,700 DAI. The user receives the difference between the strike price and the spot price (3,000  - 2,700), multiplied by the amount of options they own (2). In this case, the user receives 600 DAI on exercise.

**Exercising and settlement of a CALL option**

![Call options rise in value as the underlying token price rises in value.](../../.gitbook/assets/2.2.png)

If at the time of exercise, the price of the underlying asset is higher than the breakeven price, the call option is considered **In The Money**. In this case, the user is entitled to the payoff, which is equal to the strike price of the underlying minus the spot price. This difference is calculated automatically and settled **in the underlying asset** (the quote token) to the option buyer. \
\
**Example:** A user buys a 2 ETH/DAI call option, at a strike price of 3,500 DAI. At the time of exercise, the ETH price is 4,000 DAI. User receives the difference between the strike price and the spot price (4,000 - 3,500), multiplied by the amount of options they own (2). In this case, the user is entitled to 1,000 DAI, which is settled in ETH. Thus the user receives (1,000/4,000 ETH) = 0.25 ETH on exercise.

**NOTE:** Currently options can only be exercised back to the pool. In the near future, we will also enable selling options back to the pool.
