*Journal*  
Rasmus Groth  
*20181112, Utterslev, Copenhagen*

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
