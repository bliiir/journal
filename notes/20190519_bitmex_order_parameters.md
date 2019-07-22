## Market Buy
#### CCXT method
```py
self.exchange_client.create_order(
    symbol = "BTC/USD",
    side = "Buy",
    ordType = "market",
    amount = 1714),
    {
    "displayQty" : 0,
    "clOrdID" : "my_custom_order_id",
    "text" : "My_custom_text",
    })
```

#### Pure json
```json
{
    "symbol":"XBTUSD",
    "side" : "Buy",
    "ordType" : "Market",
    "orderQty" : 1714,
    "displayQty" : 0,
    "clOrdID" : "my_custom_order_id",
    "text" : "My_custom_text",
}
```

## Market Stop Loss

#### CCXT
```py
self.exchange_client.create_order(
    symbol = "BTC/USD",
    side = "Sell",
    ordType = "market",
    amount = 1714),
    {
        "ordType" : "Stop",
        "orderQty" : 1714:
        "stopPx" : 5895,
        "execInsts" : "ReduceOnly"
    })
```

#### Pure json
```json
{
    "symbol":"XBTUSD",
    "side" : "Sell",
    "ordType" : "Stop",
    "orderQty" : 1714,
    "stopPx" : 5895,
    "execInsts" : "Close",
    "displayQty" : 0,
    "clOrdID" : "my_custom_order_id",
    "text" : "My_custom_text",
}
```

## Market Take Profit
Assuming 50% stake off the table

#### CCXT
```py
self.exchange_client.create_order(
    symbol = "BTC/USD",
    side = "Sell",
    ordType = "market",
    amount = 1714),
    {
        "ordType" : "MarketIfTouched",
        "orderQty" : 867:
        "stopPx" : 6070,
        "execInsts" : "ReduceOnly"
    })
```

#### Pure json
```json
{
    "symbol":"XBTUSD",
    "side" : "Sell",
    "ordType" : "MarketIfTouched",
    "orderQty" : 867,
    "stopPx" : 6070,
    "execInsts" : "ReduceOnly",
    "displayQty" : 0,
    "clOrdID" : "my_custom_order_id",
    "text" : "My_custom_text",
}
