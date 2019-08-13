**Coding Journal**
**Author**: [Rasmus Groth](https://github.com/bliiir), Utterslev, Denmark
**Started**: 20180427, Utterslev, Copenhagen, Denmark
**Edited**: 20190727, Utterslev, Copenhagen, Denmark

## Python Decorators

I was reading through [this article][1] from [this series][2] and stumbled on the concept of 'decorators'. I don't really understand them so I found [this article][3] which explains in more detail. Let me try to work through it...

Apparently you can assign a function to a variable in Python. Like this:

#### Assigning functions to variables
```python
# Define the function
def greet(name):
    return("Hello " + name )

# Assign the function to a variable
say_hello = greet

# Use the say_hello instance of the greet function to call the greet function
print(say_hello("Bruce"))
```
```
Hello Bruce
```
Pretty neat. No idea why that is a good idea, but now I know.

This is possible because functions can be passed like arguments because they are 'first class citizens' in Python.

Right - on to nested function:

---

#### Define functions inside other functions

```python
# Define the parent function
def greet(name):

    # Define the child function
    def get_message():
        return "Hello "

    # Assign the child function plus name to a variable
    result = get_message()+name
    return result

# Call the greet function with "Bruce" as the argument
print greet("Bruce")
```
```
Hello Bruce
```

Neat - that means we can nest functions, and assign a function and some additional functionality to a variable like we did in the line ```result = get_message()+name```

---

#### Pass as parameters to other functions
```python
# Define first function which takes a name as input
def greet(name):
   return "Hello " + name

# Define second function which takes a function as input
def call_func(func):
    other_name = "Bruce"
    return func(other_name)

# Call second function with first function as the argument. Notice the greet does not have () at the end
print call_func(greet)
```
```
Hello Bruce
```
Pretty cool. Still not sure why I need it, but I am sure I will later when I start building more complicated stuff

---

#### Generate functions with other functions

```python
# Main function
def compose_greet_func():

    # Nested function
    def get_message():
        return "Hello Bruce"

    # Returns the get message function
    return get_message

# Store the main function in the variable greet, which when called returns the nested function
greet = compose_greet_func()

# Print the return of the greet variable that refers to the compose_greet_func
print(greet())
```
```
Hello Bruce
```

---

#### Closure
Inner functions have access to the enclosing scope

```python
# Main function
def compose_greet_func(name):

    # Nested function
    def get_message():

        # Notice how the nested function has access to 'name', which was
        # passed to the main function and not explicitly to the nested function
        return "Hello "+name

    # Calls the nested function and returns it from the main function
    return get_message

# Store the result of calling the main function with the argument "Bruce"
greet = compose_greet_func("Bruce")

# Print the stored result
print greet()
```
```
Hello Bruce
```

---

#### Composition of Decorators
Decorators are wrappers of existing functions that enable you to add to a functions
```python
## 2. fetch the get_text function without running it
def get_text(first_name, last_name):
    return "Hi, {0} {1} - how are you?".format(first_name, last_name)

# 3. Pass it to the p_decorate funtion
def p_decorate(func):

    # 5.
    def func_wrapper(first_name, last_name):

        # 6. Return the content of the argument func wrapped in
        # <p></p> tags
        return("<p>{0}</p>".format(func(first_name, last_name)))

    # 4. Invoke the func_wrapper function (5+6) and return it
    return func_wrapper

# 1. Call the p_decorate function with the get text function as the
# argument and store the object in my_get_text
my_get_text = p_decorate(get_text)

# 6. Now invoke the my_get_text instance of the p_decorate with Bruce
# and Wayne as the arguments for the get function.
print(my_get_text("Bruce", "Wayne"))

```
```
<p>Hi, Bruce Wayne - how are you?</p>
```
---


... Long story short. We want to create a bunch of functions that decorate a string. This can be done like this:

```python
# 2.Wrap the incoming input in some lorem
def get_text(name):
   return("Hello, {0} - how are you?".format(name))

# 3. Wrap the incoming input in <strong> tags
def strong_decorate(func):
    def func_wrapper(name):
        return("<strong>{0}</strong>".format(func(name)))
    return(func_wrapper)

# 4. Wrap the incoming input in <p> tags
def p_decorate(func):
   def func_wrapper(name):
       return("<p>{0}</p>".format(func(name)))
   return(func_wrapper)

# 5. # 3. Wrap the incoming input in <div> tags
def div_decorate(func):
    def func_wrapper(name):
        return("<div>{0}</div>".format(func(name)))
    return(func_wrapper)

# 1. We call the div_decorate function which we pass the p_decorate function which we pass the strong_decorate function which we pass the get_text function
get_text = div_decorate(p_decorate(strong_decorate(get_text)))

print(get_text("Bruce"))
```
```
<div><p><strong>Hello, Bruce - how are you</strong></p></div>
```
Pretty neat - I now have a good idea of what a decorator does, but here is an even neater way to work with them
```python
# 3. Wrap the incoming input in <strong> tags
def strong_decorate(func):
    def func_wrapper(name):
        return("<strong>{0}</strong>".format(func(name)))
    return(func_wrapper)

# 4. Wrap the incoming input in <p> tags
def p_decorate(func):
   def func_wrapper(name):
       return("<p>{0}</p>".format(func(name)))
   return(func_wrapper)

# 5. # 3. Wrap the incoming input in <div> tags
def div_decorate(func):
    def func_wrapper(name):
        return("<div>{0}</div>".format(func(name)))
    return(func_wrapper)

# 1. Instead of the nested function, call above, we can stack the decorators using the @ sign
# First wrap the name in the greeting, then pass it to the strong_decorate function, then pass the result to the p_decorate function, then pass the result to the div_decorate function
@div_decorate # This third
@p_decorate # This second
@strong_decorate # Do this first
def get_text(name):
   return("Hello, {0} - how are you?".format(name))

print(get_text("Bruce"))
```
```
<div><p><strong>Hello, Bruce - how are you?</strong></p></div>
```


There are more goodies in the links mentioned above.

[1]: https://medium.freecodecamp.org/learning-python-from-zero-to-hero-120ea540b567
[2]: https://medium.freecodecamp.org/python-collection-of-my-favorite-articles-8469b8455939
[3]: https://www.thecodeship.com/patterns/guide-to-python-function-decorators/
[4]: https://realpython.com/primer-on-python-decorators/
