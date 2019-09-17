## Assert methods in Python 3.2 +
[Official documentation](https://docs.python.org/3/library/unittest.html)

| Method | Checks that |
| :-- | :-- |
| **Basic** | |
| `assertEqual(a, b)` | a == b |
| `assertNotEqual(a, b)` |	a != b |
| `assertTrue(x)` |	bool(x) is True |
| `assertFalse(x)` |	bool(x) is False |
| `assertIs(a, b)` |	a is b |
| `assertIsNot(a, b)` |	a is not b |
| `assertIsNone(x)` |	x is None |
| `assertIsNotNone(x)` | 	x is not None |
| `assertIn(a, b)` |	a in b |
| `assertNotIn(a, b)` |	a not in b |
| `assertIsInstance(a, b)` |	isinstance(a, b) |
| `assertNotIsInstance(a, b)` |	not isinstance(a, b) |
| **Extended** | |
| `assertGreater(a, b)` |	a > b |
| `assertGreaterEqual(a, b)` | a >= b |
| `assertLess(a, b)` | a < b |
| `assertLessEqual(a, b)` | a <= b |
| `assertAlmostEqual(a, b)` |	round(a-b, 7) == 0 |
| `assertNotAlmostEqual(a, b)` | round(a-b, 7) != 0 |
| `assertRegex(s, r)` | r.search(s) |
| `assertNotRegex(s, r)` | not r.search(s) |
| `assertCountEqual(a, b)` | a and b have the same elements in the same number, regardless of their order |
| **Exceptions, warnings and logging** | |
| `assertRaises(exc, fun, *args, **kwds)` |	fun(*args, **kwds) raises exc |
| `assertRaisesRegex(exc, r, fun, *args, **kwds)` |	fun(*args, **kwds) raises exc and the message matches regex r |
| `assertWarns(warn, fun, *args, **kwds)` |	fun(*args, **kwds) raises warn |
| `assertWarnsRegex(warn, r, fun, *args, **kwds)` |	fun(*args, **kwds) raises warn and the message matches regex r |
| `assertLogs(logger, level)` |	The with block logs on logger with minimum level |

# Run unittests

### All
```py
python3 -m unittest discover .
```

### Single

```py
python test.py
```

#### Verbose
```py
python test.py -v
```


---

# Unit testing in Python
As explained to me by [Martin Breuss](https://github.com/martin-martin) and [Corey Shafer](https://www.youtube.com/watch?v=6tNS--WetLI)

Create a file with the name of the package or file you want to test pre-pended with 'test_' - ie:
 ```
 test_mypackage.py
 ```

  in the same folder as the file you are testing.

```py
import unittest
import myPackage # File that contains my functions

class TestMyPackage(unittest.Testcase): # Camel case (Java)

    def test_myTestMethod1(self):
        self.assertEqual(statement, value)

    def test_myTestMethod2(self):
        self.assertTrue(statement)

    ...
```
Note on syntax: Naming the test classes using camel-case is a convention from Java


Run the single test from the command line like so:

```
python3 -m unittest test_myPackage.py
```

Run all unit-tests in the current and sub-folders like so:

```
python3 -m unittest
```

Will walk down through the folder structure from where this command is initiated

Test-driven development: Write these unit-tests first and then write a script that complies with the test

## Repetition

### By case
In order to avoid doing repetitive work for each test case, like retreiving a table from a database, you can use ```setUp()``` and ```tearDown()```

```py
    def setUp(self):
        # executes before every single test case
        pass

    def tearDown(self):
        # executes after every single test case
        pass
```
This will repeat for each test case (```def```) inside a suite (```class```)

The code would look like this:
```py
import unittest
import myPackage # File that contains my functions

class TestMyPackage(unittest.Testcase): # Camel case (Java)

    def setUp(self):
        # executes before every single test case
        pass

    def tearDown(self):
        # executes after every single test case
        pass

    def test_myTestMethod1(self):
        self.assertEqual(statement, value)

    def test_myTestMethod2(self):
        self.assertTrue(statement)

    ...
```

### By suite
In order to avoid doing repetitive work for the test-suite, like connecting to a database, you can use ```setUpClass()``` and ```tearDownClass()```

```py
    @classmethod
    def setUpClass(cls):
        pass

    @classmethod
    def tearDownClass(cls):
        pass
```
This will repeat for each test suite (```class```) inside the test file.

The code would look like this:

```py
import unittest
import myPackage # File that contains my functions

class TestMyPackage(unittest.Testcase): # Camel case (Java)

    def setUp(self):
        # executes before every single test case
        pass

    def tearDown(self):
        # executes after every single test case
        pass

    @classmethod
    def setUpClass(cls):
        # Executes when the class is instantiated
        pass

    @classmethod
    def tearDownClass(cls):
        # Executes when all the test cases have been run
        pass

    def test_myTestMethod1(self):
        self.assertEqual(statement, value)

    def test_myTestMethod2(self):
        self.assertTrue(statement)

    ...
```
