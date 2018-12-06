# REST API design pattern

## Categories

- Coins
- Currencies (fiats)
- Exchanges
- Markets (pairs)
- Tickers
- Info
- Common, aggregates and other

## Output data by category

---

### Coins

#### Last state

Show latest coin stat.

Method: GET

Url: /coin/latest

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| coin             | false    | string | all     |
| convert currency | false    | string | USD     |

Data:

- Price\_\<currency>
- Market_cap
- Volume\_\<currency>
- Change\_\<period>\_\<currency>

Data json one:

```json
{
  "price_to": "value",
  "market_cap": "value",
  "volume_24h": "value",
  "volume_to_24h": "value",
  "volume_7d": "value",
  "volume_to_7d": "value",
  "volume_30d": "value",
  "volume_to_30d": "value",
  "change_24h": "value",
  "change_7d": "value",
  "change_30d": "value",
  "timestamp": "time"
}
```

Data json all:

```json
{
  "coin name": {
    "price_to": "value",
    "market_cap": "value",
    "volume_24h": "value",
    "volume_to_24h": "value",
    "volume_7d": "value",
    "volume_to_7d": "value",
    "volume_30d": "value",
    "volume_to_30d": "value",
    "change_24h": "value",
    "change_7d": "value",
    "change_30d": "value",
    "timestamp": "time"
  }
}
```

#### Historical

Show historical data

Method: GET

Url: /coin/historical

Options:

| Name       | Required | Type                 | Default      |
| ---------- | -------- | -------------------- | ------------ |
| coin       | true     | string               |              |
| quote      | false    | string               | all          |
| start from | false    | time (unix)          | 0            |
| end        | false    | time (unix)          | current time |
| period     | false    | string (5m, 1d, etc) | 1d           |

Data json:

```json
[
  {
    "coin name": {
      "price_to": "value",
      "volume": "value",
      "volume_to": "value",
      "timestamp": "time"
    }
  },
  {
    "coin name": {
      "price_to": "value",
      "volume": "value",
      "volume_to": "value",
      "timestamp": "time"
    }
  }
]
```

#### Trade places

Show exchanges and pairs, where you can trade that coin.

Method: GET

Url: /coin/exchange-markets

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| coin             | true     | string |         |
| exchange         | false    | string | all     |
| convert currency | false    | string | USD     |

Data json:

```json
{
  "exchange name 1": {
    "pair name 1": {
      "volume_24h": "value",
      "volume_to_24h": "value",
      "volume_7d": "value",
      "volume_to_7d": "value",
      "volume_30d": "value",
      "volume_to_30d": "value",
      "change_24h": "value",
      "change_7d": "value",
      "change_30d": "value"
    },
    "pair name 2": {
      "volume_24h": "value",
      "volume_to_24h": "value",
      "volume_7d": "value",
      "volume_to_7d": "value",
      "volume_30d": "value",
      "volume_to_30d": "value",
      "change_24h": "value",
      "change_7d": "value",
      "change_30d": "value"
    }
  },
  "exchange name 2": {
    "pair name 1": {
      "volume_24h": "value",
      "volume_to_24h": "value",
      "volume_7d": "value",
      "volume_to_7d": "value",
      "volume_30d": "value",
      "volume_to_30d": "value",
      "change_24h": "value",
      "change_7d": "value",
      "change_30d": "value"
    },
    "pair name 2": {
      "volume_24h": "value",
      "volume_to_24h": "value",
      "volume_7d": "value",
      "volume_to_7d": "value",
      "volume_30d": "value",
      "volume_to_30d": "value",
      "change_24h": "value",
      "change_7d": "value",
      "change_30d": "value"
    }
  }
}
```

#### Exchanges

Show exchanges, which trade this coin.

Method: GET

Url: /coin/exchanges

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| coin             | true     | string |         |
| convert currency | false    | string | USD     |

Data:

- Exchange name
- Relative pairs with volume to currency (1d, 7d, 30d)

Data json:

```json
[
  {
    "exchange name": "name",
    "volume_24h": "value",
    "volume_to_24h": "value",
    "volume_7d": "value",
    "volume_to_7d": "value",
    "volume_30d": "value",
    "volume_to_30d": "value",
    "change_24h": "value",
    "change_7d": "value",
    "change_30d": "value"
  },
  {
    "exchange name": "name 2",
    "volume_24h": "value",
    "volume_to_24h": "value",
    "volume_7d": "value",
    "volume_to_7d": "value",
    "volume_30d": "value",
    "volume_to_30d": "value",
    "change_24h": "value",
    "change_7d": "value",
    "change_30d": "value"
  }
]
```

#### Markets

Show aggregated pairs with that coin.

Method: GET

Url: /coin/markets

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| coin             | true     | string |         |
| convert currency | false    | string | USD     |

Data:

- Pairs with volume to currency (1d, 7d, 30d)

Data json:

```json
[
  {
    "pair name": "name",
    "volume_24h": "value",
    "volume_to_24h": "value",
    "volume_7d": "value",
    "volume_to_7d": "value",
    "volume_30d": "value",
    "volume_to_30d": "value",
    "change_24h": "value",
    "change_7d": "value",
    "change_30d": "value"
  }
]
```

### Exchanges

#### Info

Show exchange information.

Method: GET

Url: /exchanges/info

Options:

| Name     | Required | Type   | Default |
| -------- | -------- | ------ | ------- |
| exchange | false    | string |         |

Data:

- ???
- available

#### Markets

Show pairs, which traded at exchange.

Method: GET

Url: /exchange/markets

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| exchange         | true     | string |         |
| convert currency | false    | string | USD     |

Data json:

```json
[
  {
    "pair name": "name",
    "last_trade_price_to": "value",
    "high_price_24h": "value",
    "low_price_24h": "value",
    "last_trade_volume_to": "volume",
    "volume_24h": "value",
    "volume_24h_to": "value",
    "change_to_24h": "value",
    "timestamp": "time"
  }
]
```

#### Aggregates

Show aggregated exchange info.

Method: GET

Url: /exchange/global

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| exchange         | false    | string | all     |
| convert currency | false    | string | USD     |

Data json:

```json
{
  "volume_24h": "value",
  "volume_to_24h": "value",
  "volume_7d": "value",
  "volume_to_7d": "value",
  "volume_30d": "value",
  "volume_to_30d": "value",
  "change_24h": "value",
  "change_7d": "value",
  "change_30d": "value",
  "available": true,
  "timestamp": "time"
}
```

#### Historical

Show exchange pairs history.

Method: GET

Url: /exchange/candles

Options:

| Name       | Required | Type                 | Default      |
| ---------- | -------- | -------------------- | ------------ |
| exchange   | true     | string               |              |
| markets    | true     | string               |              |
| start from | false    | time (unix)          | 0            |
| end        | false    | time (unix)          | current time |
| period     | false    | string (5m, 1d, etc) | 1d           |

Data json:

```json
[
  {
    "open": "value",
    "close": "value",
    "high": "value",
    "low": "value",
    "volume": "value",
    "volume_quote": "value",
    "timestamp": "time"
  },
  {
    "open": "value",
    "close": "value",
    "high": "value",
    "low": "value",
    "volume": "value",
    "volume_quote": "value",
    "timestamp": "time"
  }
]
```

### Currencies

#### Exchanges

Show exchanges, which trade to that currency whit markets.

Method: GET

Url: /currency/markets

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| currency         | true     | string |         |
| quote            | false    | string | all     |
| convert currency | false    | string | USD     |

Data json:

```json
[
  {
    "exchange name": "name",
    "volume_24h": "value",
    "volume_24h_to": "value",
    "change_24h": "value",
    "change_to_24h": "value"
  }
]
```

### Markets

#### Global

Show market global trade data.

Method: GET

Url: /market/global

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| market           | true     | string |         |
| convert currency | false    | string | USD     |

Data json:

```json
[
  {
    "volume_24h": "value",
    "volume_to_24h": "value",
    "volume_7d": "value",
    "volume_to_7d": "value",
    "volume_30d": "value",
    "volume_to_30d": "value",
    "change_24h": "value",
    "change_7d": "value",
    "change_30d": "value",
    "timestamp": "time"
  }
]
```

### Tickers

#### Latest

Show last relative tickers.

Method: GET

Url: /market/tickers

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| market           | true     | string |         |
| exchange         | false    | string |         |
| convert currency | false    | string | USD     |

Data json:

```json
[
  {
    "market": "name",
    "exchange": "name",
    "ask": "value",
    "ask": "value",
    "last_trade_price_to": "value",
    "high_price_24h": "value",
    "low_price_24h": "value",
    "volume_24h": "value",
    "volume_24h_to": "value",
    "timestamp": "time"
  }
]
```

#### Weight average

Show weight average tickers.

Method: GET

Url: /ticker/average

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| market           | true     | string |         |
| convert currency | false    | string | USD     |

Data json:

```json
[
  {
    "ask": "value",
    "ask": "value",
    "last_trade_price_to": "value",
    "high_price_24h": "value",
    "low_price_24h": "value",
    "volume_24h": "value",
    "volume_24h_to": "value",
    "timestamp": "time"
  }
]
```

### Info

#### Coins

Show currency information.

Url: /info/currency

Options:

| Name | Required | Type   | Default |
| ---- | -------- | ------ | ------- |
| coin | false    | string |         |

Data:

- ???

#### Exchanges

Show exchange information.

Method: GET

Url: /info/exchange

Options:

| Name     | Required | Type   | Default |
| -------- | -------- | ------ | ------- |
| currency | true     | string |         |

Data:

- ???

#### Markets exchanges

Show exchanges, which trade specified market.

Method: GET

Url: /info/market/exchange

Options:

| Name   | Required | Type   | Default |
| ------ | -------- | ------ | ------- |
| market | true     | string |         |

Data:

```json
["exchange1", "exchange2", "etc"]
```

#### Exchange markets

Show exchanges, which trade specified market.

Method: GET

Url: /info/exchange/market

Options:

| Name     | Required | Type   | Default |
| -------- | -------- | ------ | ------- |
| exchange | true     | string |         |

Data:

```json
["market1", "market2", "etc"]
```

### Common

#### Global markets info (latest)

Show global data.

Method: GET

Url: /global/latest

Options:

| Name             | Required | Type   | Default |
| ---------------- | -------- | ------ | ------- |
| convert currency | false    | string | USD     |

Data json:

```json
{
  "cryptocurrencies": 10000,
  "markets": 10000,
  "exchanges": 1000,
  "updated_at": "time",
  "total_market_cap": 1000,
  "total_volume": 1000,
  "timestamp": "time"
}
```

#### Global markets info (historical)

Show global data.

Method: GET

Url: /global/historical

Options:

| Name             | Required | Type                     | Default      |
| ---------------- | -------- | ------------------------ | ------------ |
| convert currency | false    | string                   | USD          |
| convert currency | false    | string                   | USD          |
| start from       | false    | time (unix)              | 0            |
| end              | false    | time (unix)              | current time |
| period           | false    | string (1m, 5m, 1d, etc) | 1d           |

Data json:

```json
[
  {
    "cryptocurrencies": 10000,
    "markets": 10000,
    "exchanges": 1000,
    "total_market_cap": 1000,
    "total_volume": 1000,
    "timestamp": "time"
  },
  {
    "cryptocurrencies": 10000,
    "markets": 10000,
    "exchanges": 1000,
    "total_market_cap": 1000,
    "total_volume": 1000,
    "timestamp": "time1"
  }
]
```
