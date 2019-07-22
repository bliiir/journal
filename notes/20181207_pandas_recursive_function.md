*Journal*
Rasmus Groth
*20181207, Utterslev, Copenhagen, Denmark*

[The dataframe I am working on from](https://www.dropbox.com/s/n3npkq6cs3s3wtd/momentum_signals.csv?dl=0)

[The Stackoverflow answer that finally got me on the right track track](https://stackoverflow.com/a/41073207/9536012)

Attempt #3 below worked :)

# Pseudocode

```py
# The fraction of the total capital to spend on each trade
limit = 1

# How much leverage to trade with
leverage = 1

# Hold
If signal = 0
base = base[1]
quota = quoate[1]

# Long
If signal = 1
quota = quota - limit * quota
base = base + (quota * limit * leverage ) / price_open

# Short
If signal = -1
base = base - limit * base
quota = quota + base * limit * leverage * price_open)
```

# Attempt 1
```py
pd.options.mode.chained_assignment = None  # default='warn'

limit = 0.5
leverage = 1

init_base = 1
init_quote = 1000

df['base'] = np.nan
df['quote'] = np.nan

hold = df['signal'] == 0
long = df['signal'] >= 1
short = df['signal'] <= -1

# Initial conditions
df.at[0,'base'] = 1
df.at[0,'quote'] = 1000

# Hold
df.at[hold,'base'] = df['base'].shift(1)
df.at[hold,'quote'] = df['quote'].shift(1)

# # Long
df.at[long,'quote'] = df['quote'].shift(1) - df['quote'].shift(1) * limit * leverage
df.at[long,'base'] = df['base'].shift(1) + df['quote'].shift(1) * limit * leverage / df['price_open']

# # Short
df.at[short,'base'] = df['base'].shift(1) - df['base'].shift(1) * limit * leverage
df.at[short,'quote'] = df['quote'].shift(1) + df['base'].shift(1) * limit * leverage * df['price_open']

df.head()
```

# Attempt 2

```py
pd.options.mode.chained_assignment = None  # default='warn'

limit = 1
leverage = 1

df['base'] = np.nan
df['quote'] = np.nan

df['base'].iloc[0:] = 1
df['quote'].iloc[0:] = 1000

# Signal 0
df['base'].loc[df['signal'] == 0] = df['base'].shift(1)
df['quote'].loc[df['signal'] == 0] = df['quote'].shift(1)

# Signal 1
df['quote'].loc[df['signal'] == 1] = (df['quote'].shift(1)) - (df['quote'].shift(1) * limit)
df['base'].loc[df['signal'] == 1] = (df['base'].shift(1)) + (df['quote'].shift(1) / df['price_open'] * limit)

# Signal -1
df['base'].loc[df['signal'] == -1] = (df['base'].shift(1)) - (df['base'].shift(1) * limit)
df['quote'].loc[df['signal'] == -1] = (df['quote'].shift(1)) + (df['base'].shift(1) / df['price_open'] * limit)

df.head()
```

# Attempt 3
```py
def b(row):
    if row['signal'] >= 1: return row['base'] * 2
    elif row['signal'] <= -1: return row['base'] / 2
    else: return row['base'].shift(1)

def q(row):
    if row['signal'] >= 1: return row['quote'] / 2
    if row['signal'] <= -1: return row['quote'] * 2
    else: return row['quote'].shift(1)

df['base'] = df.apply(b, axis=1)
df['quote'] = df.apply(q, axis=1)
```
