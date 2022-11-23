---
description: >-
  Liquidity providers have granular control over what strategies to underwrite,
  enabling custom risk profile selection.
---

# Providing Liquidity

Each asset pair has 2 pools: a **Call pool** and a **Put pool**. Calls pools are underwritten in the underlying asset (WBTC, ETH, LINK) and puts pools are currently underwritten in DAI. This allows both liquidity providers to granularly decide which pool they'd like to underwrite and option buyers to select which direction they'd like to trade. The best of both worlds.

Each pool is described by the following parameters:\
\
**Asset pair**\
**Total amount of assets**\
**Utilization ratio**&#x20;

****\
****The **C-level** is **** the liquidity adjustment pricing coefficient, specific to each pool.\
****(Please see the [C-level Overview section](../optimal-pricing-algorithm/option-pricing/capital-pricing-initial-liquidity-not-an-issue/) for more details. Intuitively - the higher the C value, the more expensive it is to purchase options from the pool, and the higher return the LPs get.)

![Liquidity pools on Premia are user-managed and asset/direction specific.](<../../.gitbook/assets/4 (1).png>)

**Example:** If liquidity provider is bearish on ETH and bullish on LINK, they can \
**1.** Underwrite ETH calls, by placing ETH in the ETH/DAI call pool\
**2.** Underwrite LINK puts by placing DAI in LINK/DAI put pool

Alternatively, users can select any asset they'd like to deposit and use the [Smart Deposit router](smart-deposit-router.md) to select the optimal pools based on all of the pool C-levels and total liquidity.
