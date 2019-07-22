## Decorators
A decorator is a function that takes a function AS an argument and changes its behaviour
```py
def decorator_func(initial_func):

    def wrapper_func():
        print("wrapper function picked ome...")
        return initial_func()

    return wrapper_func

# Long version
def prettify():
    print("flowers for you")
prettify = decorator_func(prettify)

# Short version - means that you call decorator_func every time you call prettify
@decorator_func
def prettify():
    print("flowers for you")

@decorator_func
def feed():
    print("Apples and potatoes")

prettify()
feed()
```
Output
```
wrapper function picked ome...
flowers for you
wrapper function picked ome...
Apples and potatoes
```

*20180919*

## Scope

```py
name = "Mycroft"                #01
                                #02
def box():                      #03
    print(name)                 #04
                                #05
    def smaller_box():          #06
        name = "martin"         #07
        print(name)             #08
                                #08
        def smallest_box():     #09
            print(name)         #10
                                #11
        smallest_box()          #12
                                #13
    smaller_box()               #14
                                #15
box()                           #16
                                #17
print(name)                     #18
```

#### Result
```
>>> Mycroft
>>> martin
>>> martin
>>> Mycroft
```
#### Explanation
* Initialize
* 01: Set `name` to "Mycroft"
* 17: call `box()`
    * 03: execute `box()`
        * 04: `print(name)` > Mycroft
        * 15: call `smaller_box()`
            * 06: execute `smaller_box()`
                * 07: set `name` to "martin"
                * 08: `print(name)` > martin
                * 13: call `smallest_box()`
                    * 10: execute `smallest_box()`
                        * 11: `print(name)` > martin
* 19: `print(name)` > Mycroft (because we are in the global scope)
