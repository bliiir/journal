*Journal*
Rasmus Groth
*20181031, Utterslev, Copenhagen, Denmark*

# Documentation
> Readability is a primary focus for Python developers, in both project and code documentation. Following some simple best practices can save both you and others a lot of time.
>
>[Python-guide.org](https://docs.python-guide.org/writing/documentation/)

## Comments
Comments are developer notes, intended to be read with the code, but not be included in the documentation  
[pep-0008](https://www.python.org/dev/peps/pep-0008/#comments)

### Docstrings
>A docstring is a string literal that occurs as the first statement in a module, function, class, or method definition. Such a docstring becomes the __doc__ special attribute of that object.  
>[pep-0257](https://www.python.org/dev/peps/pep-0257/)

Docstrings are intended to be used in documentation and therefore have a structure to them:

#### Structure
```py
class My_class(arg1, arg2):
    '''Summary

        Args:
            :param (int) arg1:
            :param (int) arg2:

        Returns:
            :return (int:
    '''

    ...
```
#### Example
```py
class Manufacturer():

    def __init__(company_name, number_of_employees):
        '''Car manufacturer object

            Args:
                :param (str) company_name: The name of the manufacturer company
                :param (int) number_of_employees: The number of employess if the manufacturer

            Returns:
                :return (dict): Dictionary with company name as the key and number of employees as the value
            '''
        ...
```

Docstrings can be used to autogenerate documentation using for example [Sphinx](http://www.sphinx-doc.org/en/master/) if structured in the [reStructuredText](http://docutils.sourceforge.net/rst.html) format.

Here are some [examples](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html) from Google.

It is not neccesary to document variables in the docstring if [typehints](https://www.python.org/dev/peps/pep-0484/) are used throughout the code

[More on docstrings](https://www.python.org/dev/peps/pep-0257/#specification)


### Epytext
Another format like reStructuredText  
http://epydoc.sourceforge.net/epytextintro.html
