*Cheatsheet*
Rasmus Groth
*Started: 20190123, Utterslev, Copenhagen, Denmark*
*Edited: 20190821, Utterslev, Copenhagen, Denmark*

# Exception handling

| Command | Description |
| :-- | :-- |
| `try: <statement>` | try to execute the statement |
| `except: <statement>` | If there is an exception, execute statment |
| `except ZeroDivisionError AS zde: <statement>` | If there is a zero division error, execute statement |
| `else: <statement>` | Do this if there are no exceptions |
| `finally: \n\t statement` | Do this in all cases |
| `assert (<statement>), "message"` | Throws a custom statement when an exception happens |
| `raise Exceptionclass("message")` | Raises an error of Exceptionclass with a message |


## Examples

### Try, except, else, finally
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
Output
```
Cannot access that element
Done
```

```py
try:
    if(10 < 0):
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
def load_page(url):
    pass

class MyException(Exception):

    status_codes = {404: "page not found", 500: "server error"}

    def __init__(self, status_code, message):
        self.status_code = status_code
        self.message = message
        self.status_message = MyException.status_codes[status_code]

    def __str__(self):
        return "This is a new way to return the exception AS a string"


url = 'our_site/page_that_does_not_exist.html'

try:
    if (url != 'our_site/page_that_does_exist.html'):
        raise MyException(404, "exception raised")
    page = load_page(url)

except MyException as exc:
    print("error with status code: ", exc.status_code)
    print("with message: ", exc.message)
    print(exc.status_message)

```
Output
```
error with status code:  404
with message:  exception raised
page not found
```