---
description: Work in Progress
---

# Technical Reference

<figure><img src="../.gitbook/assets/architectural-engineering-home-construction-new-york-city-artframe-royalty-free-under-construction-removebg-preview (2).png" alt="" width="333"><figcaption></figcaption></figure>

### <mark style="color:blue;">Overview</mark>

### <mark style="color:blue;">Types & Entities</mark>

**Token**

**PriceOracle**

**Pair**

**Pool**

**Position**

**Option**

**Liquidity**

**Vault**

**Trade**

**Quote**

**Tick**

**TradeSide**

**Margin**

**MarginPool**

**MarginPosition**

**MarginTrade**

**MarginQuote**

**MarginLiquidity**

V**ePremia**

**VePremiaToken**

**VePremiaPosition**

**VePremiaVote**

**VePremiaGauge**

**Vault**

### <mark style="color:blue;">Read Functions</mark>

**get\_token(address: string, chain\_id: int): Token**

**get\_all\_tokens(chain\_id: int): Token\[]**

**get\_token\_price(token: Token): Decimal**

**get\_pair(base: Token, quote: Token, oracle: PriceOracle): Pair**

**get\_pairs(token: Token, is\_quote?: bool, oracle?: PriceOracle): Pair\[]**

**get\_all\_pairs(chain\_id: int): Pair\[]**

**get\_pool(pair: Pair, strike: Decimal, maturity: int, is\_call: bool): Pool**

**get\_pools(pair: Pair, strike?: Decimal, maturity?: int, is\_call?: bool): Pool\[]**

**get\_all\_pools(chainId: int): Pool\[]**

**get\_position(pool: Pool, user\_address: string, lower: int, upper: int): Position**

**get\_positions(pool: Pool, user\_address?: string): Position\[]**

**get\_all\_positions(chainId: int): Position\[]**

**get\_option(pool: Pool, user\_address: string, side: TradeSide): Option**

**get\_options(pool: Pool, user\_address?: string, side?: TradeSide): Option\[]**

**get\_all\_options(chainId: int): Option\[]**

**get\_tick(pool: Pool, index: int): Tick**

**get\_ticks(pool: Pool, lower?: int, upper?: int): Tick\[]**

**get\_taker\_fee(pool: Pool): Decimal**

**get\_refundable\_gas\_fee(pool: Pool, contract\_interface: string): Decimal**

**get\_market\_price(pool: Pool): Decimal**

**get\_claimable\_fees(pool: Pool, position: Position): Decimal**

**get\_position\_liquidity(pool: Pool, position: Position): Liquidity**

**get\_quote(pool: Pool, side: TradeSide, size: Decimal): Quote**

**get\_next\_maturity(pool: Pool): int**

**get\_closest\_strike(pool: Pool): Decimal**

**Margin**

**get()….**

**VePremia**

**get()….**

**Vaults**

**get()….**

### <mark style="color:blue;">Write Functions</mark>

**claim\_fees(pool: Pool, position: Position): Decimal**

**trade\_then\_deposit(pool: Pool, position: Position, max\_price: Decimal, deadline: int): Trade**

**deposit(pool: Pool, position: Position)**

**withdraw(pool: Pool, position: Position, liquidity: Liquidity)**

**update\_position(pool: Pool, position: Position, liquidity: Liquidity)**

**trade(pool: Pool, owner: string, operator: string, side: TradeSide, size: Decimal, max\_price: Decimal, deadline: int): Trade**

**trade(pool: Pool, owner: string, operator: string, quote: Quote, max\_slippage: Decimal, deadline: int): Trade**

**fill\_quote(pool: Pool, owner: string, operator: string, quote: Quote, max\_price: Decimal, deadline: int): Trade**

**annihilate(pool: Pool, owner: string, liquidity: Liquidity)**

**transfer\_position(pool: Pool, position: Position, new\_owner: string, new\_operator: string, liquidity: Liquidity)**

**transfer\_option(pool: Pool, option: Option, new\_owner: string, new\_operator: string, liquidity: Liquidity)**

**exercise(pool: Pool, option: Option, owner: string, operator: string, refund\_address?: string): Decimal**

**settle(pool: Pool, option: Option, owner: string, operator: string, refund\_address?: string): Decimal**

**settle\_position(pool: Pool, position: Position, refund\_address?: string): Decimal**

**Margin**

**add()…**

**VePremia**

**add()…**

**Vaults**

**add()…**

### <mark style="color:blue;">Enums</mark>

### <mark style="color:blue;">Interfaces</mark>
