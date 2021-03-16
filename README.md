# simpleBinance
Лёгкий rest-клиент для получения информации по стоимости покупки/обмена криптовалют

Более полную информацию можно получить https://binance-docs.github.io/apidocs/spot/en/

Пример использования

```php
// Exchange information::Current exchange trading rules and symbol information
\Thelema\Crypto\Binance::getInstance()->get('exchangeInfo');
```

```php
// Order book
\Thelema\Crypto\Binance::getInstance()->get('depth', 'ETHBTC', 5);
```

```php
// Recent trades list::Get recent trades
\Thelema\Crypto\Binance::getInstance()->get('trades', 'ETHBTC', 5);
```

```php
// Old trade lookup (MARKET_DATA)::Get older trades.
\Thelema\Crypto\Binance::getInstance()->get('historicalTrades', 'ETHBTC', 5);
```

```php
// 24hr ticker price change statistics::24 hour rolling window price change statistics.
// Careful when accessing this with no symbol.
\Thelema\Crypto\Binance::getInstance()->get('ticker/24hr', 'ETHBTC');
```

```php
// Symbol price ticker::Latest price for a symbol or symbols.
\Thelema\Crypto\Binance::getInstance()->get('ticker/price', 'ETHBTC');
```

```php
// Symbol order book ticker::Best price/qty on the order book for a symbol or symbols.
\Thelema\Crypto\Binance::getInstance()->get('ticker/bookTicker', 'ETHBTC')
```

```php
// Current average price for a symbol
\Thelema\Crypto\Binance::getInstance()->get('avgPrice', 'ETHBTC');
```

```php
// Compressed/Aggregate trades list::Get compressed, aggregate trades. Trades that fill at the time, from the same taker order, with the same price will have the quantity aggregated.
// [
//  {
//    "a": 26129,         // Aggregate tradeId
//    "p": "0.01633102",  // Price
//    "q": "4.70443515",  // Quantity
//    "f": 27781,         // First tradeId
//    "l": 27781,         // Last tradeId
//    "T": 1498793709153, // Timestamp
//    "m": true,          // Was the buyer the maker?
//    "M": true           // Was the trade the best price match?
//  }
//]
\Thelema\Crypto\Binance::getInstance()->get('aggTrades', 'ETHBTC', '10');
```
