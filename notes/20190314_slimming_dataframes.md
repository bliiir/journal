# Slimming down the dataframes
 - only th 'id' column from the input should remain

## Model

### Database
- [x] ccat.model.database.client.py
- [x] ccat.model.database.instrument.py
- [x] ccat.model.database.market.py
- [x] ccat.model.database.timeframe.py
- [x] ccat.model.database.bucket.py

### Exchange
- [x] ccat.model.exchange.exchange.py
- [x] ccat.model.exchange.order.py


## View
 - [ ] NA

## Controller

### Feature
- [x] ccat.controller.feature.height.py

### helper
- [x] ccat.controller.helper.df_magic.py
- [x] ccat.controller.helper.df_x_df.py
- [x] ccat.controller.helper.df_x_val.py
- [x] ccat.controller.helper.time.py

### Indicator
- [x] ccat.controller.indicator.ema.py
- [x] ccat.controller.indicator.rsi.py
- [x] ccat.controller.indicator.sma.py

### Signal
- [x] ccat.controller.signal.overtraded.py
- [x] ccat.controller.signal.reversal.py
- [x] ccat.controller.signal.extreme.py

### Strategy
- [x] ccat.controller.signal.momentum.py
