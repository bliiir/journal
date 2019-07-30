**Coding Journal**
Author: [Rasmus Groth](https://github.com/bliiir)
Started: 20190130, Utterslev, Copenhagen, Denmark
Edited: 20190730, Utterslev, Copenhagen, Denmark

# Map, filter and reduce
Based on [this][1] Socratica tutorial

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
Simpler using map


[1]:<https://www.youtube.com/watch?v=hUes6y2b--0> "Socratica on map, filter, reduce"
