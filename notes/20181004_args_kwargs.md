## \*args and \*\*kwargs

### Args - arguments

> args are used when you don't know how many arguments you are passing. The name of the args variable is preceeded with a * to tell python it is a tuple of arguments.
Args are a bit like lists

```py
def my_function(*unicorn):
    sum = 0
    for i in unicorn:
        sum += 1s
    print("count:", sum)
    #print(a,b)

my_function(1, 2, 3, 4, 10, 30)
```

`>>> count: 6`

### Kwargs - key-word-arguments
\*\*kwargs are used when you don't know how many arguments you are passing, but each argument is named unlike args
Kwargs are a bit like dictionaries
```py
def my_kwargs_function(**kwargs):
    print(kwargs)

my_kwargs_function(x=1, y=2, z=3, a=4, b=10, c=30)
```
`>>> {'x': 1, 'y': 2, 'z': 3, 'a': 4, 'b': 10, 'c': 30} `

```
