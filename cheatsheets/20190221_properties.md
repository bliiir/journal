# Getting object properties and attributes

| Command | Description |
| :-- | :-- |
| [`id()`](https://docs.python.org/3.7/library/functions.html#id) | Return the “identity” of an object. This is an integer which is the address of the object in memory.|
| [`type()`](https://docs.python.org/3.7/library/functions.html#type) | Return the type of an object. The return value is a type object and generally the same object as returned by object.__class__. |
| [`dir()`](https://docs.python.org/3.7/library/functions.html#dir) | Without arguments, return the list of names in the current local scope. With an argument, attempt to return a list of valid attributes for that object |
| [`vars()`](https://docs.python.org/3.7/library/functions.html#vars) | Return the __dict__ attribute for a module, class, instance, or any other object with a __dict__ attribute. |
| [`globals()`](https://docs.python.org/3.7/library/functions.html#globals) | Return a dictionary representing the current global symbol table |
| [`locals()`](https://docs.python.org/3.7/library/functions.html#locals) | Update and return a dictionary representing the current local symbol table |
| [`inspect.currentframe()`](https://docs.python.org/3/library/inspect.html#inspect.currentframe) | Return the frame object for the caller’s stack frame. |
| `object.keys` | Get the keys of a dictionary object |