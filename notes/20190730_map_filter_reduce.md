**Coding Journal**
Author: [Rasmus Groth](https://github.com/bliiir)
Started: 20190130, Utterslev, Copenhagen, Denmark
Edited: 20190730, Utterslev, Copenhagen, Denmark

# Map, filter and reduce
Based on [this][1] Socratica tutorial

## Map

The `map(f, data)` returns an iterator with the function `f` to applied to each element of the dataset `data`

>Data: $a_1, a_2, ..., a_n$
>Function: $f$
>map($f$, $data$) returns an iterator over $f(a_1)$, $f(a_2)$, ..., $f(a_n)$

### Example 1
#### Method 1
```py
import math

def area(r):
    '''Area of circle with radius `r`'''
    return math.pi * (r*2)

# List of radii to turn into areas
radii = [2, 5, 7.1, 0.3, 10]

# Initialize empty list of areas
areas = []

for r in radii:
    a = area(r)
    areas.append(a)

print(areas)
```

#### Method 2
```py
import math, pdb

def area(r):
    '''Area of circle with radius `r`'''
    return math.pi * (r*2)

# List of radii to turn into areas
radii = [2, 5, 7.1, 0.3, 10]

# Map the list of radii to the area function
areas = map(area, radii)

# Convert the map object to a list and print it
print(list(areas))
```
### Example 2
```py
celcius = [
    ("Berlin", 29),
    ("Cairo", 36),
    ("Buenos Aires", 19),
    ("Los Angeles", 26),
    ("Tokyo", 27),
    ("New York", 28),
    ("London", 22),
    ("Beijing", 32)
    ]

celcius_to_fahrenheit = lambda temp_c: (temp_c[0], (9/5) * temp_c[1] + 32)

fahrenheit = list(map(celcius_to_fahrenheit, celcius))

print(fahrenheit)
```



[1]:<https://www.youtube.com/watch?v=hUes6y2b--0> "Socratica on map, filter, reduce"
