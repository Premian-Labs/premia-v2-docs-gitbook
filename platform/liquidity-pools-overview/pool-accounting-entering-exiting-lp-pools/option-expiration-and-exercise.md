---
description: >-
  An option can complete its lifecycle in one of two ways: either be exercised
  or expire worthless.
---

# Option Expiration and Exercise

When an option is exercised, the same transaction settles the position - the option holder receives the payoff, and the newly freed capital is returned to the pool. If an option expires without being exercised, the value of the option at expiration is locked in the option, allowing the option to be processed by any user of the pool. Users (or Chainlink Keepers) can call `processExpired` on the pool to automatically free capital in the next expired option and send the exercise reward to the option holder. This ensures the pools stay maximally capital efficient and users always receive the best returns possible.

_Premia utilizes automated tools such as Chainlink Keepers to process expired options daily, to ensure maximal capital efficiency and the best user experience for users of the protocol._

Liquidity providers' capital is organized on deposit into Free Capital intervals, to ensure the fair sequencing of underwritten options. When an option is settled, for the newly freed capital to be returned to a Free Capital interval, it either has to exceed the minimum interval requirement for a new interval to be created, or the LP needs to have an existing Free Capital interval.&#x20;

![Option collateral is added back to a liquidity provider's interval queue, if larger than the minimum interval size.](<../../../.gitbook/assets/10 (1).png>)

1. If the LP has an existing Free Capital interval, the newly freed capital is added to this interval (the amount is increased).&#x20;
2. If the LP has no existing Free Capital intervals, then should the newly freed capital exceed the minimum interval requirement, it is added at the back of the queue.

However, if the LP does not have an existing Free Capital interval, and the newly freed capital is below the minimum interval requirement, it will be placed in an **intermediate pool** until enough capital is accumulated to meet the minimum interval requirement. The reason behind imposing a minimum interval requirement, is to avoid unbounded capital fragmentation (think an option buyer having to scan 1,000 intervals worth 1 DAI each, to buy a single option). This ensures gas prices stay optimal for users of the protocol.

**Liquidity providers can still withdraw their liquidity from their intermediate pool at any time.**
