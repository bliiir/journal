# Exception handling

| Command | Description |
| :-- | :-- |
| `try: \n\t statement` | try to execute the statement |
| `except: \n\t statement` | If there is an exception, execute statment |
| `except ZeroDivisionError AS zde: \n\t statement` | If there is a zero division error, execute statement |
| `else: \n\t statement` | Do this if there are no exceptions |
| `finally: \n\t statement` | Do this in all cases |
| `assert (statement), "message"` | Throws a custom statement when an exception happens |
| `raise Exceptionclass("message")` | Raises an error of Exceptionclass with a message |


```py
# Try this
try:
    _list = [1,2]
    print(_list[3])

# Catch index errors specifically
except IndexError AS ie:
    print("Cannot access that element")

# Catch all other exceptions
except Exception AS exc:
    print("There was an exception:", exc)

# Do this if no exceptions
else:
    print("There were no errors")
# Always do this
finally:
    print("Done")
```
```
Cannot access that element
Done
```

```py
try:
    if(10 > 0):
        my_exception = Exception("We are raising this exception")
        raise Exception

except Exception:
    print("There was an error", my_exception)
```
```
There was an error We are raising this exception
```

### Custom exception handling
```py
class MyException(Exception):

    status_codes = {404: "not found", 500: "server error"}

    def __init__(self, status_code, message):
        self.status_code = status_code
        self.message = message
        self.status_message = MyException.status_codes[status_code]

    def __str__(self):
        return "This is a new way to return the exception AS a string"

x = 10
y = 0

try:
    if (y == 0):
        raise MyException(404, "exception raised")
    print(x/y)

except MyException AS exc:
    print("error with status code: ", exc.status_code)
    print("with message: ", exc.message)
    print(exc.status_message)

```
