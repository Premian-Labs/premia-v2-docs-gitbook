# Query Examples

Below are some sample queries you can use to gather information from the Hop contracts.

You can build your own queries using a [GraphQL Explorer](https://graphiql-online.com/graphiql) and enter your endpoint to limit the data to exactly what you need.

## Token Pools

* Get the pools for a specific token address. _Note: token address should be all lowercase_

```graphql
query tokenPools(
  $Asset: String = "0x0bc529c00c6401aef6d220be8c6ea1667f6ad93e"
) {
  pools(where: { underlying: $Asset }) {
    averageStrike
    averageReturn
    averageMaturity
    minTokenAmount
    netDeposited
    netSize
    netSizeInUsd
    openInterest
    openInterestInUsd
    optionType
    pairName
    startBlock
    startTimestamp
    totalAvailable
    totalCharged
    totalCloseLoss
    totalClosed
    totalDeposited
    totalExerciseLoss
    totalExercised
    totalFeesEarned
    totalLocked
    totalPremiumsEarned
    totalPremiumsEarnedInUsd
    totalSellLoss
    totalSold
    totalVolume
    totalVolumeInUsd
    totalWithdrawn
    utilizationRate
    underlying {
      id
      name
    }
  }
}
```

## Get User's Options

* Get the options for a specific wallet address

```graphql
query UserOptions(
  $User: String = "0x022e3ce4eda264b3e3fef62036c8182ceb88e6ce"
) {
  userOwnedOptions(where: { user: $User }) {
    id
    user
    size
    totalClosed
    totalCloseReturn
    totalExercised
    totalExerciseReturn
    totalFeesPaid
    totalSellReturn
    totalSold
    totalSpent
    totalSpentUSD
    profitLossPercentage
    lastTradeTimestamp
    maturity
    option {
      strike
      strikeInUsd
      optionType
      pairName
    }
  }
}
```

## PremiaTVL Timeseries

* Get the daily TVL for the last 30 days for the protocol

```graphql
query DailyTVL {
  totalTVLDailies(
    first: 30
    orderBy: timestamp
    orderDirection: desc
    where: { id_not: "all/last" }
  ) {
    timestamp
    totalValueLockedInUsd
    id
  }
}
```
