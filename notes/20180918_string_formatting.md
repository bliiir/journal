# String formatting

```py
hi = "Hello"
you = "Rasmus"
```

##### The old way
```py
print("I say %s" % hi)
>>> I say Hello
```
##### The new way - `.format`
```py
print("I say {:20s} to {}".format(hi, you))
>>> I say Hello                to Rasmus
```

##### The hip way - f strings
```py
print(f"I say {hi:20s} to {you}")
>>> I say Hello                to Rasmus
```
