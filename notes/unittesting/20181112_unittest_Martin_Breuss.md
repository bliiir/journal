# Python's `unittest` module

Filename it with `test_yourpackagename.py`

Keep the file with your other files
Because allows to see them all together

Descriptive test class name
Names for the tests should start with

```py
def test_yourtestmethodname(self):
    pass
```

(The naming is because that’s how `unittest` knows what to pick up)

Informs the test runner that these are tests

```py
import yourpackage
import unittest


def TestYourPackage(unittest.TestCase):
    # define your tests as methods in here
    pass
```

Always remember to inherit from `unittest.TestCase`


The essential piece of a test is to `assert` for expected results, often using:

```py
# expects the two inputs to be the same
assertEquals(yourfunctioncall(arg1, arg2), expected_result)

# expects the defined error to be raised
with assertRaises(ValueError):
    yourfunctioncall(arg1, arg2)
```

Always add to your tests when you figure out some bug you didn’t think
about before.
Update the test case so that the test would now fail if not taken care of.
That assures that you won't run into the same issue again later on.


## Taking out repetitive parts

### Wrapping every single test case

```py
    def setUp(self):
        # executes before every single test case
        pass

    def tearDown(self):
        # executes after every single test case
        pass
```

As mentioned in the comments, `setUp` will be run before every single test,
`tearDown` afterwards.


### Wrapping the whole test suite
```py
    @classmethod
    def setUpClass(cls):
        pass

    @classmethod
    def tearDownClass(cls):
        pass
```

These two methods get run once at the very beginning/end of testing.

## Executing `unittest`s

Run it with:

`python -m unittest [test_yourpackagename.py]`

Adding the filename of your test file is optional, since `unittest` does
test discovery and looks to run all files starting with `test_`.

Alternatively you can also add:

```py
if __name__ == '__main__':
    unittest.main()
```

to the bottom of the test file, and then run it directly with:

`python test_yourpackagename.py`


# Other testing frameworks in Python

Another favorite (but external) package is `pytest`.
It’s a wrapper around `unittest`, that allows to write *functions* instead
of needing to define a *class* with *methods*.

It also allows to use the `assert` keyword directly.
