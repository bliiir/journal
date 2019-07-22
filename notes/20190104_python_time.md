*Journal*
Rasmus Groth
*20190104, Utterslev, Copenhagen, Denmark*

# Time in Python (sucks)
But the [datetime module](https://docs.python.org/3/library/datetime.html) makes it easier by handling dates and time in an object that can then be returned in different formats

## Datetime
An object with attributes and methods

```py
import datetime
t = datetime.datetime.utcnow()
t
```
Output:
```
datetime.datetime(2019, 1, 4, 13, 49, 28, 701252)
```
A datetime object.

### Datetime Object > Unix Timestamp
```py
tu = t.timestamp()
tu
```
Output:
```
1546606168.701252
```
This is the Unix epoch. The Unix epoch (or Unix time or POSIX time or Unix timestamp) is the number of seconds that have elapsed since January 1, 1970.

### Unix Timestamp > Datetime Object
```py
datetime.datetime.utcfromtimestamp(tu)
```
Output:
```
datetime.datetime(2019, 1, 4, 12, 49, 28, 701252)
```

### Methods
See available methods [here](https://docs.python.org/3/library/datetime.html).

#### Examples
##### [Date](https://docs.python.org/3/library/datetime.html#datetime.date)
```py
t.date()
```
Out:
```
datetime.date(2019, 1, 4)
```

##### [String from time](https://docs.python.org/3/library/datetime.html#datetime.date.strftime)
```py
t.strftime("%Y.%M.%d %H:%M:%S")
```
Out:
```
'2019.49.04 13:49:28'
```
[Here](https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior) is a list of formatting options
