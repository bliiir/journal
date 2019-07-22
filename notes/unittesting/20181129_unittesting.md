# Unittesting

### Structure of a project with unittests

    new_project
    ├── antigravity
    │   ├── __init__.py
    │   └── antigravity.py
    └── test
        ├── __init__.py
        └── test_antigravity.py


### Naming conventions

##### Files
```
test_name.py
```

##### Classes
```py
class Test_verbose_and_descriptive_test_name(unittest.TestCase)
```

##### Methods
```py
def test_name(self):
```
---

### Structure of a unittest module
[This](https://stackoverflow.com/a/24266885/9536012 ) answer on Stackoverflow is great.

Official documentation [here](https://docs.python.org/3/library/unittest.html).

Using the [Arrange, Act, Assert pattern](http://wiki.c2.com/?ArrangeActAssert):

```py
import unittest
import my_module

class Test_A(unittest.TestCase):

    def test_1(self):
        # Arrange
        my_string = 'Abc'

        # Act
        lowercase = my_module.my_method(user_input)

        # Assert
        self.assertEqual(lowercase, 'abc')


if __name__ == '__main__':
    unittest.main()
```

### Assert variants
```py
self.assertEqual('foo'.upper(), 'FOO')
self.assertTrue('FOO'.isupper()
self.assertFalse('Foo'.isupper())

```

Example
```py
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```

### Run all unittests inside the ```new_project``` directory
```
cd new_project
python -m unittest discover
```

### Run a single testcase
```
$ cd new_project
$ python -m unittest test.test_antigravity
```
