# Guides

### <mark style="color:blue;">Quick Start</mark>

The **full SDK** is free to use and open-source, currently available in the following languages:

* **Python**
* **Typescript / Javascript**

\<aside> 💡 The full SDK can be used trustlessly to execute any action or query any data from the protocol.

\</aside>

To use the full SDK from Python:

```python
pip install premia-v3
```

Example:

```python
from premia_v3 import Position
```

To use the full SDK from Typescript / Javascript:

```python
npm install @premia/v3
```

or

```python
yarn add @premia/v3
```

Example:

```tsx
import Position from "@premia/v3"
```

The **API-based SDK** is also free to use and open-source, currently available in the following languages:

* **Java / Kotlin**
* **Go**
* **C#**
* **Ruby**
* **Swift**
* **PHP**

\<aside> 💡 The API-based SDK requires sending wallet credentials securely over HTTPS to our server to execute any action. Alternatively, the SDK can print out necessary transaction parameters, such that users can execute transactions themselves using standard tooling in the language of their choice, without sending credentials to a server.

\</aside>

To use the API-based SDK from any of the above languages, install the `premia-v3` (or `@premia/v3` where name-spacing is enabled) package from your language’s package manager. You can find the source and documentation for all API-based SDKs [here](https://google.com).

### <mark style="color:blue;">Initialization</mark>

To query on-chain data with the SDK, you will need to a `provider_uri`.

```python
from premia_v3 import SDK

providerURI = "INSERT_YOUR_PROVIDER_URI_HERE"
premia = SDK(provider_uri)
```

To execute actions on chain using the SDK, you will additionally need to provide a `wallet_key`, the private key to the wallet you would like to sign transactions with.

```python
from premia_v3 import SDK

provider_uri = "INSERT_YOUR_PROVIDER_URI_HERE"
wallet_key = "INSERT_YOUR_PRIVATE_KEY_HERE"
premia = SDK(provider_uri, wallet_key)
```

\<aside> 💡 Alternatively, one can run their own node (Geth, Parity, etc.) locally and store the private key(s) within the node. Using a local node’s `provider_uri` with stored private keys does not require passing in a `wallet_key`.

\</aside>

Once a `Provider` has been initialized, data can be queried from on-chain and actions can be executed within the protocol, from your attached wallet.

```python
from premia_v3 import SDK, Token, Pair, Pool, Quote, TradeSide
from decimal import Decimal
from time import time

provider_uri = "INSERT_YOUR_PROVIDER_URI_HERE"
private_key = "INSERT_YOUR_PRIVATE_KEY_HERE"
wallet_address = "INSERT_YOUR_WALLET_ADDRESS_HERE"
premia = SDK(provider_uri, private_key, wallet_address)

base_token_address = "INSERT_STABLE_TOKEN_ADDRESS_HERE"
quote_token_address = "INSERT_VOLATILE_TOKEN_ADDRESS_HERE"
quote_to_base_price_oracle_address = "INSERT_PRICE_ORACLE_ADDRESS_HERE"
chain_id = 1 # <---- Update to the chain you are using

base: Token = premia.get_token(
	address=base_token_address,
	chain_id=chain_id
)
quote: Token = premia.get_token(
	address=quote_token_address,
	chain_id=chain_id
)

pair: Pair = premia.get_pair(
	base=base,
	quote=quote,
	oracle=quote_to_base_price_oracle_address,
)
closest_strike = pair.get_closest_strike()
next_maturity = pair.get_next_maturity(strike=closest_strike)

pool: Pool = pool.get_pool(
	strike=closest_strike,
	maturity=next_maturity,
	is_call=True
)

quote: Quote = pool.get_quote(
	side=TradeSide.BUY,
	size=Decimal(1.5)
)

trade: Trade = pool.trade(
	owner=premia.signer.address,
  operator=premia.signer.address,
	quote=quote,
	max_slippage=1.05, # 5% max slippage
	deadline=int(time()) + 60 * 5 # 5 minute deadline
)
```

### <mark style="color:blue;">Pool</mark>

*   Creating a Pool Instance

    To initialize a `Pool`, you first need to initialize the corresponding `Pair`.

    ```python
    from premia_v3 import SDK, Pair, Pool

    provider_uri = "INSERT_YOUR_PROVIDER_URI_HERE"
    private_key = "INSERT_YOUR_PRIVATE_KEY_HERE"
    wallet_address = "INSERT_YOUR_WALLET_ADDRESS_HERE"
    premia = SDK(provider_uri, private_key, wallet_address)

    quote_symbol = "ETH"
    chain_id = 1 # <---- Update to the chain you are using
    all_pairs = premia.get_all_pairs(chain_id=chain_id)

    for _pair in all_pairs:
    	if pair.quote.symbol == quote_symbol:
    		pair = pair
    		break
    ```

    Once you have your `Pair`, it is simple to `get_all_pools` for the `Pair` or to get a specific `Pool`:

    ```python
    all_pools = pair.get_pools()

    # OR

    strike = pair.get_closest_strike()
    maturity = pair.get_next_maturity(strike=strike)
    pool = pair.get_pool(
    	strike=strike,
    	maturity=maturity,
    	is_call=True
    )
    ```

    From here, data such as option prices and liquidity levels can be queried from the `pool`, or trades and LP actions can be executed.
*   Getting a Quote

    Option prices can be queried from a `Pool` if you know the `size` (number of option contracts) they would like to trade.

    ```python
    from premia_v3 import Quote, TradeSide
    from decimal import Decimal

    quote: Quote = pool.get_quote(
    	side=TradeSide.BUY,
    	size=Decimal(1.5)
    )
    ```

### <mark style="color:blue;">Executing a Trade</mark>

To trade an option, you can either get a `Quote` first, or if you already know the price, you can directly create the `Trade`:

```python
from premia_v3 import Quote, Trade, TradeSide
from decimal import Decimal
from time import time

quote: Quote = pool.get_quote(
	side=TradeSide.BUY,
	size=Decimal(1.5)
)

trade: Trade = pool.trade(
	owner=premia.signer.address,
  operator=premia.signer.address,
	quote=quote,
	max_slippage=1.05, # 5% max slippage
	deadline=int(time()) + 60 * 5 # 5 minute deadline
)

# OR

price = Decimal(0.2)
max_slippage = 1.05 # 5% max slippage

trade: Trade = pool.trade(
	owner=premia.signer.address,
  operator=premia.signer.address,
	side=TradeSide.BUY,
	size=Decimal(1.5),
	max_price=price * max_slippage,
	deadline=int(time()) + 60 * 5 # 5 minute deadline
)
```

### <mark style="color:blue;">Routing a Trade</mark>

### <mark style="color:blue;">Pool Liquidity</mark>

*   Creating a Liquidity Position

    To create a market-making liquidity position, `deposit` into the option `Pool` that you want to buy and/or sell options in.

    ```python
    from premia_v3 import Position, TradeSide, Address
    from decimal import Decimal

    market_price = pool.get_market_price()

    position = Position(
    	owner=Address(wallet_address),
      operator=Address(wallet_address),
      lower=pool.get_minimum_tick_distance(), # min tick
      upper=market_price,
      side=TradeSide.SELL,
      collateral=Decimal("1.0"), # 1.0 units of collateral
      contracts=Decimal("0.5") # 0.5 long contracts to SELL (to close)
    )

    pool.deposit(position=position)

    # OR

    position = Position(
    	owner=Address(wallet_address),
      operator=Address(wallet_address),
      lower=market_price,
      upper=Decimal("1.0"), # max tick
      side=TradeSide.BUY,
      collateral=Decimal("1.0"), # 1.0 units of collateral
      contracts=Decimal("0.5") # 0.5 short contracts to BUY (to cover)
    )

    pool.deposit(position=position)
    ```
* Modifying a Liquidity Position
* Collecting Fees

### <mark style="color:blue;">Collecting Fees</mark>

### <mark style="color:blue;">Creating and Managing Vault Positions</mark>

### <mark style="color:blue;">Staking PREMIA</mark>

### <mark style="color:blue;">Advanced Usage</mark>
