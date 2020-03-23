Journal, Rasmus Groth
*Started: 20181122, Copenhagen, Denmark*
*Edited: 20200129, Lyngby, Denmark*

# Python packages

## Installing packages

From outside python

| command | Description |
| :-- | :-- |
| `pip install plotly` | Installs plotly on the machine using pypip.org (Python pip installs packages) |
| `pip install ...` | TODO: Get info from mark about how to set up a local folder with the packages |


## Using Packages
From inside python

| Command | Description |
| :-- | :--
| `import packagename` | Imports the package | packagename.methodname()
| `from packagename import methodname` | imports the method so it is available without the packagename AS if it was a function writting in the local script| methodname() |
| `import packagename as pn` | Imports packagename AS pn | `pn.methodname()` |
| `from packagename import methodname as mn` | Imports methodname from packagename into the alias mn | `mn()` |


## Making packages

Set up your directory structure.

```shell
package_wrapper/
│── package/
│	│── __init__.py
│	│── module.py
│	│── subModule/
│	│	│── __init__.py
│	│	│──	module.py
│   │   └── subSubModule/
│	│		│──	__init__.py
│	│		│──	module.py
│	│		└──	module.py
│	│── tests/
│	│	│──	test_module.py
│	│	│──	test_subModule.py
│	│	└──	test_subSubModule.py
│	└──	docs/
│		└── module_diagram.graphml
│── setup.py
│── README.md
│── MANIFEST.in
└── LICENSE
```

The `__init__.py` files are what makes Python recognize the directory as a module

The `setup.py` file should look something like this:

```python
from setuptools import setup, find_packages

setup(
    name='<name>',
    version='<version>',
    description='<description>',
    url='<url>',
    author='<author>',
    author_email='<email>',
    license='<license>',
    packages=find_packages(<directory>),
	package_dir={
    install_requires=[
          '<package>',
          '<package>'
	],
    zip_safe=False
    )
```


Use import statements in the topmost directory to make imports further down in the package easier. Like this

The `__init__.py` file in the `package` directory should look like this:

```py
name = '<package>'
import <package>.<subpackage>.<subsubpackage>.<...>.<file>.<class> as <shortname>
```

Then if you want to reference a module from one sub-package in another sub-package you can do this:
```py
import <package>.<shortname>
```
Instead of:
```py
import <package>.<subpackage>.<subysubpackage>.<...>.<file>.<class> as <shortname>
```
Every time.

Put an empty The `__init__.py` in each of the folders of the package you are making.


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
```py
python3 -m pip install --user --upgrade setuptools wheel
```
Run this command from the directory that the setup.py file is in:
```
python3 setup.py sdist bdist_wheel
```
This creates a `dist` folder in the package

Now lets install/upgrade Twine

```sh
pip3 install twine
```
And/or:

```sh
python3 -m pip3 install --user --upgrade twine
```

Now upload your package:
```sh
 twine upload dist/*
```

That's it!

## Installing from a private pypi server
```sh
pip install --extra-index-url <url> ppi_lib
```


## References
- [Official Python Package Tutorial][[official_python_package_tutorial]]
- The [Hitchhiker's Guide to packaging][hitchhikers_guide_to_packaging] is great.
- [This guide on Medium (How to write your own Python Package and publish it on PyPi)][medium_how_to_publish_your_own_python_package] is also pretty good.
- So is [this medium guide (How to upload your python package to PyPi)][medium_how_to_upload_your_python_to_pypi]
- [This better scientific software doc][betterscientificsoftware_python_pypi_packaging] is also pretty good.
- Setting up a PyPI repo: from [Linode docs 'create python package repo'][linode_how_to_create_a_private_python_package_repository].
- Creating an executable script: Use `scripts`: from [Stack Overflow create a python executable using setuptools][SO_create_python_executable]
- Adding an executable command without '.py': Use `entry_points` and `console_scripts`: from [Chris Warriks blog][chriswarrick_python_apps_the_right_way]
- Using a third party package repo: Use `dependency_links`: [Stack Overflow Extra python package index][SO_user_extra_python_package_index]
- [Adding Non-Code Files][adding_non_code_files]
​

[SO_user_extra_python_package_index]: https://stackoverflow.com/questions/24443583/using-an-extra-python-package-index-url-with-setup-py
[hitchhikers_guide_to_packaging]: https://the-hitchhikers-guide-to-packaging.readthedocs.io/en/latest/quickstart.html
[linode_how_to_create_a_private_python_package_repository]: https://www.linode.com/docs/applications/project-management/how-to-create-a-private-python-package-repository/
[SO_create_python_executable]: https://stackoverflow.com/questions/16742203/create-a-python-executable-using-setuptools
[chriswarrick_python_apps_the_right_way]: https://chriswarrick.com/blog/2014/09/15/python-apps-the-right-way-entry_points-and-scripts/
[medium_how_to_publish_your_own_python_package]: https://medium.com/@thucnc/how-to-publish-your-own-python-package-to-pypi-4318868210f9
[betterscientificsoftware_python_pypi_packaging]: https://betterscientificsoftware.github.io/python-for-hpc/tutorials/python-pypi-packaging/#uploading-to-testpypi
[medium_how_to_upload_your_python_to_pypi]: https://medium.com/@joel.barmettler/how-to-upload-your-python-package-to-pypi-65edc5fe9c56
[official_python_package_tutorial]: https://packaging.python.org/tutorials/packaging-projects/
[adding_non_code_files]: https://python-packaging.readthedocs.io/en/latest/non-code-files.html




pip install --extra-index-url https://ostracion.intomics.com/ ppi_lib
pip install ppi_cli


Is this public? Authentication?!?


To upload the package to a private pip server
python3 setup.py sdist bdist_wheel upload -r ostracion
