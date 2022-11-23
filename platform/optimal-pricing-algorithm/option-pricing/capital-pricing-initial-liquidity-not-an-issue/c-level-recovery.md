---
description: >-
  The pools are smart enough to recognize and recover from unstable c-level
  states.
---

# C-level Recovery

There are a few possible states a pool can get into that can be considered **unstable**. What this means, simply, is that the pool c-level is at a point compared to the pool utilization rate that causes less trades to be made, compared to equilibrium and less deposits to be incentivized, compared to equilibrium. These states are:

* **A high relative pool c-level, with a low pool utilization rate**
* **A low relative pool c-level, with a high pool utilization rate**

These two situations result in unstable pool convergence. As such, the c-level is able to mathematically "realize" when it is in such a situation and steadily correct itself back to a more stable state over time. This means that as no pool updates are made, the pool c-level will automatically trend back towards a more stable level, if not already stable.

Specifically, we can treat the C-level like a temperature gauge, where each change in pool liquidity either increases or decreases the temperature of the system (option purchases would increase the temperature, pool deposits would decrease the temperature). Then in situations where the C-level gets into an unstable state (such as high C-level with low pool utilization, or low C-level with high pool utilization) we can allow the C-level to naturally converge toward an ambient temperature (steady state), so long as there is no interaction with the system for a certain length of time (i.e. no trades or deposits are made).

In a more concrete example, let's say the C-level was very high, but the pool was highly under-utilized (such as after the initial deposit). If after time there are no buyers, the pool C-level will automatically begin to come down to incentivize the next buyer and recover from this unstable state. Vice versa would happen in the opposite situation, where C-level is very low and there is very-little free liquidity.
