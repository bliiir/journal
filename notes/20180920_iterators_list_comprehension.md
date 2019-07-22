## Iterators

I will use this list throughout these examples:

```py
num_list = list(range(1,20))
```

### `enumerate():`

```py
_list = ["plant", "animal", "bacteria", "funghi"]
for index, value in enumerate(_list, start=1):
    print(index, value)
```

```
0 plant
1 animal
2 bacteria
3 funghi
```

```py
for i in range(len(_list)):
    print(i, _list[i])
```

```
0 plant
1 animal
2 bacteria
3 funghi
```

## List comprehension

### Long version

```py
new_list = []
for item in num_list:
    if item % 2 == 0:
        new_item = item ** 2
        new_list.append(new_item)
print(new_list)
```
`>>> [4, 16, 36, 64, 100, 144, 196, 256, 324]`

### Short version
```py
new_list = [item**2 for item in num_list if item % 2 == 0]
print(new_list)
```
`>>> [4, 16, 36, 64, 100, 144, 196, 256, 324]`

### Generators
Generators creates an iterable that can be activated ON the fly, but does not keep a persistent object with values

```py
gen = (n**2 for n in nums)
for i in gen:
    print(i)



## Lambda functions
Generate a list of the squares for each of the items in the list below
```py
_list = [1,2,3]
```
### Normal functions
```py
def square(x):
    return x**2

res = list(map(square, _list))
print(res)
```
Output
```
[1, 4, 9]
```

### Lambda function
```py
res = list(map(lambda x: x**2, _list))
print(res)
```
Output
```
[1, 4, 9]
```

### List comprehension
```py
res = [x**2 for x in _list]
print(res)
```
Output
```
[1, 4, 9]
```

