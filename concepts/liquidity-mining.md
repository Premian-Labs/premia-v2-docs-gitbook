# Liquidity Mining

## <mark style="color:blue;">Overview</mark>

*
*
* Explain the purpose of liquidity mining is to subsidize liquidity and grow protocol volume/revenue, while decentralizing ownership of token to real users of the platform
* Probably give a small history on successful liquidity mining, including Curve and Premia v2

## <mark style="color:blue;">Vault Allocation</mark>

* Works the same as V2, except instead of voting on individual pools, users will vote on individual vaults.
  * Each chain gets allocated specific amount of PREMIA emissions per day (e.g. 5,000 PREMIA for Arbitrum).
  * Users with vxPREMIA on Arbitrum can vote on any vault to send a portion of their influence to that vault.
  * Total emissions per vault are determined based on total chain emissions and the percentage of voting points each vault has (from 0% to 100%).
  * More vxPREMIA staked and longer stake increases voting influence.
* Rewards are continuously distributed in PREMIA pro-rata, ad-valorem to users in the pool (more size + longer deposit = more rewards) each block.

## <mark style="color:blue;">Future Pool Allocation</mark>

* Users will be able to vote on liquidity mining emissions to individual token pairs
* Rewards for each token pair will be distributed across pools, based on their proximity to near-term, ATM options and the effectiveness of liquidity in each pool
* Release date TBD

### Distribution over Volatility Surface

* The point is to incentivize liquidity to move where it will most likely be traded against
* Process details TBD
