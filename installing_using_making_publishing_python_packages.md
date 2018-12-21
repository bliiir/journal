*Journal*  
Rasmus Groth  
*20181122, Utterslev, Copenhagen*

# Python packages

## Installing packages

From outside python

| command | Description |
| :-- | :-- |
| `pip install plotly` | Installs plotly on the machine using pypip.org (Python pip installs packages) |

## Using Packages
From inside python

| Command | Description |
| :-- | :--
| `import packagename` | Imports the package | packagename.methodname()
| `from packagename import methodname` | imports the method so it is available without the packagename AS if it was a function writting in the local script| methodname() |
| `import packagename AS pn` | Imports packagename AS pn | `pn.methodname()` |
| `from packagename import methodname AS mn | Imports methodname from packagename into the alias mn | `mn()` |


## Making backages

Set up your directory structure.

```
/package_wrapper
    setup.py
    README.md
    LICENSE
    /package
        __init__.py
        module.py
        /subpackage
            __init__.py
            module.py
            subsubpackage
                ...
```

The setup.py file should look something like this:

```py
from setuptools import setup, find_packages

setup(
    name='{name}',
    version='{version}',
    description='{description}',
    url='{url}',
    author='{author}',
    author_email='{email}',
    license='{license}',
    packages=find_packages(),
    install_requires=[
          '{package}',
          '{package}'
      ],
    zip_safe=False
    )
```


Use import statements in the topmost directory to make imports further down in the package easier. Like this

The ```__init__.py``` file in the ```package``` directory should look like this:
```py
name = '{package}'
import {package}.{subpackage}.{subsubpackage}.{...}.{file}.{class} as {shortname}
```
Then if you want to reference a module from one sub-package in another sub-package you can do this:
```py
import {package}.{shortname}
```
Instead of:
```py
import {package}.{subpackage}.{subsubpackage}.{...}.{file}.{class} as {shortname}
```
Every time.

Put an empty The ```__init__.py``` in each of the folders of the package you are making.

## Install locally

Ok, assuming your package is sorted, lets install it locally

In the terminal, go to the directory with the setup.py file and write:
```
pip install -e .
```
Installs the current directory as a package with symlinks in the current environment.

You can now use your package locally.


## Putting your package on pypi.org
[Check out this tutorial](https://packaging.python.org/tutorials/packaging-projects/)

...

Upgrade setuptools wheel
```
python3 -m pip install --user --upgrade setuptools wheel
```
Run this command from the directory that the setup.py file is in:
```
python3 setup.py sdist bdist_wheel
```
This creates a ```dist``` folder in the package

Now lets install/upgrade Twine

```
pip3 install twine
```
And/or:

```
python3 -m pip3 install --user --upgrade twine
```

Now upload your package:
```
 twine upload dist/*
 ```

That's it!
