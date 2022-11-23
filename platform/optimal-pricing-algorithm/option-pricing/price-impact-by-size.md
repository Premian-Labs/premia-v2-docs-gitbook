---
description: >-
  Premia pools disincentivize highly disruptive trades through size price
  impact.
---

# Price Impact by Size

After every transaction, the pool price level updates from $$C_t \rarr C_{t+1}$$, depending on the size and the direction of the trade. This results in either an increased or decreased price for the next buyer/underwriter. There are no obvious reasons to disincentivize larger blocks of provided liquidity (on the LP side), however, whale-buying behavior needs to be accounted for.&#x20;

Suppose a whale is waiting on the sidelines for the C-level to fall below their perceived market equilibrium, just to scoop up 50% of the pool's liquidity. Such a trade would cause a significant pool price level disruption; this disruption needs to be accounted for in the price charged to the whale. If the starting value is $$C_t$$, and the ending value (post whale trade) becomes $$C_{t+1}$$, s.t. $$C_{t+1} > C_{t}$$, what price impact penalty should be imposed on the whale?

In discrete form, the whale would end up paying $$BS(V_i)* \frac{(C_t+C_{t+1})}{2}$$, however the differential form is slightly more accurate:&#x20;

**Note:** $$x_t=\frac{(S_{t+1}-S_t)}{max(S_{t+1};S_t)}$$ or more intuitively - the normalized step size, relative to the free capital in the pool.

Putting it all together, using $$C^*_t=C_t \text{ adjusted for slippage}$$ and $$\alpha=1.0$$ as a potential future trade-specific steepness modifier, we get a final pricing function:

$$
P_{t}(V_i;C_t)=BS(V_i)*C^*_t
\\
s.t.\hspace{0.25cm}C^*_t=C_t*\int^0_{x_t}e^{-x} \alpha_x*(\frac{1}{0-x_t})
$$

**This ensures large traders have no advantage over smaller traders.**
