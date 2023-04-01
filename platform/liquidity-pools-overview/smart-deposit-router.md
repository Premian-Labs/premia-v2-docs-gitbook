---
description: A tool to manage pools deposits in a liquidity and pricing optimized manner.
---

# Smart Deposit Router

The Smart Deposit feature is based on a standard mathematical procedure called portfolio optimization.

The user submits a total amount for deposit and a market sentiment, and the Smart Deposit computes the fraction of the deposit to be swapped and allocated per pool. Once determined, these allocations are recommended to the user.

![An example of a user depositing funds to pools using the Smart Deposit feature.](<../../.gitbook/assets/5 (1).png>)

The user is prompted to select a series of assets which they own, and is then prompted to select their market sentiment. The market sentiment selection has one of three settings: "bullish", "bearish", and "neutral". These settings determine which pools will be considered for deposit: calls, puts, or both.

The total value of their assets is then summed into a single nominal amount. The fractional pool allocations are then determined based on "mean-variance" criterion with respect to the aggregate pool c-values.

The allocations recommended to the user simultaneously maximize the mean c-value and minimize the variance of the c-value across the selected pools, hence they are said to satisfy the "mean-variance" criterion. The c-value is a Premia-specific pool metric which summarizes the utility value of deposits in each pool. Because each c-value summarizes the utility value of its respective pool, the smart deposit recommends an allocation that maximizes the mean c-value across pools, hence maximizing the average utility of the user's deposit.

Severe fluctuations in c-value are assumed _a priori_ to be undesirable, hence the smart-deposit feature recommends an allocation which minimizes the statistical variance of the c-value across pools.
