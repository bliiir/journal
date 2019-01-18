*Journal*  
Rasmus Groth  
*20181116, Utterslev, Copenhagen, Denmark*

This post can also be found in blog-form [here](https://medium.com/@bliiir/postgres-table-merge-using-a-triple-composite-key-f99874b073bd)

## Insert one overlapping table into another slightly different table in Postgres without duplicates

##### TL;DR
Insert a table into another with **no** single unique keys by using the ```create unique constraint``` postgres command.

---

Some context - I am a serial entrepreneur and junior Python developer building an automated crypto/algo trading platform. I am living out a lifelong dream of learning to write proper code and applying it to crypto because I am deeply bought into and very excited about the fundamentals of the space - not so much because of the trading, but because I like the society it aims to facilitate.

---
#### The Setup

Back to the topic: I have a script that pulls time-series data from the Bitmex crypto-exchange - candles as they are lovingly called. Bitmex calls them 'buckets'. I chose Bitmex because proper margin trading is a must if you are serious about trading.

I have a table called ```bucket``` in my postgres database ([This](https://launchbylunch.com/posts/2014/Feb/16/sql-naming-conventions/) really helpful post explains why it is called ```bucket``` singular). This is one of the core tables in the database as it will be hosting data on all markets, timeframes and exchanges. Preventing duplicate entries is crucial for the operation of the platform.

#### Separation of Concerns
Whenever I pull new candles from the exchange I get the 100 latest and to prevent duplicates in the main ```bucket``` table, I store them in a table called ```bucket_temp``` with the intention of merging the ```bucket_temp``` data into the ```bucket``` table. I did consider writing a Python script to do it, but I did not want to loop over the data in Python because it seemed inefficient. SQL is super-optimized for such tasks and speed is important for the platform.

The ```bucket``` table looks like this:

![](https://www.dropbox.com/s/260uvy63ysw5lp9/Screenshot%202018-11-17%2001.04.17.png?raw=1)

The ```bucket_temp``` is created using the [```to_sql()```](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_sql.html) command on a pandas dataframe.

The command looks like this:
```
self.df_buckets.to_sql('bucket_temp', con=ngn.get(), if_exists="replace")
```
And the table looks like this:

![](https://www.dropbox.com/s/bvoori9mkd3353y/Screenshot%202018-11-17%2001.03.26.png?raw=1)

### The challenge
##### There is no single index I can use to merge the data with.
As there are several timeframes (1m, 5m, 15m, 1h etc), and several markets (symbol (ie BTCUSD) + Exchange (ie Bitmex)) I have to use a combination of timeframe, market and closing time to allow for the same market, timeframes and closing times but not all at the same time.
##### The order of the columns is not the same
My own doing and I could fix that, but I don't want to depend on layout for stability, and I think this is a fun challenge.

I looked at a lot of tutorials and Stackoverflow topics and there wasn't much out there on the topic so I thought I'd stick my neck out and show what I did. [This](https://stackoverflow.com/a/37995758/9536012) Stackoverflow post put me on the right track.

### The solution
##### Create a composite index
In order to use multiple keys in my ON CONFLICT statement later, I have to create a unique index of the three keys mentioned above.

Like this:
```
create unique index merge_index on bucket (market_id, timeframe_id, time_close);
```

##### Insert the data
Now I can do a simple(ish) insert of the data from ```bucket_temp``` into the ```bucket``` table.

Like this:
```
INSERT INTO bucket(
    market_id,
    timeframe_id,
    time_close,
    price_open,
    price_high,
    price_low,
    price_close,
    volume)
    SELECT
        market_id,
        timeframe_id,
        time_close,
        price_open,
        price_high,
        price_low,
        price_close,
        volume
        FROM bucket_temp
            ON CONFLICT (market_id, timeframe_id, time_close) DO NOTHING;
```
I am pretty sure I could have done this in a much better way using SQLalchemy or another ORM, and I probably will capitulate pretty soon, but for now I had fun figuring it out.

Hope this helps you - let me know what words/tags you used to find the post so I can make it easier to find for others.
