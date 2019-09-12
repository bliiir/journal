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
