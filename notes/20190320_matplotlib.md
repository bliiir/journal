*Journal*
Rasmus Groth
*Utterslev, Copenhagen, Denmark*

Started: 20190320
Edited: 20190320

# Matplotlib

Two ways to do plots

## Setup
### Imports
```py
import numpy as np
import matplotlib.pyplot as plt
```
### Configure Matplotlib
```py
%matplotlib inline
plt.style.use('seaborn-whitegrid')
```

### Dummy data
```py
a = 2
b = 3
c = 4

xs = [x for x in range(25)]
ys = [b*x + c for x in range(25)]
zs = [a*x**2 + b*x + c  for x in range(25)]
```

## Quick and dirty
```py
# Create a figure with with 2 rows, 1 column and you will be working on the first row
plt.subplot(2,1,1)

# Give Matplotlib the data
plt.plot(xs, ys)

# Give the plot a title
plt.title('my plot')

# Add another subplot and tell Matplotlib that you will be working on the second row
plt.subplot(2,1,2)

# Give Matplotlib the data
plt.plot(zs, ws)

# Give the plot a title
plt.title('my other plot')

# Show the plot
plt.show()

```

## More control
Matplotlib uses the word 'axes' to describe a sub-figure

```py
# Create an instance of the class subplot with one figure and two axes
fig, ax = plt.subplot(2)

# Create a plot of xs and ys in the first axes
ax[0] = (xs, ys)

# Create a plot of xs and zs in the second axes
ax[1] = (xs, zs)
```

# Links
[I followed this video](https://www.youtube.com/watch?v=6rKe2IEIu8c)
[Matplotlib diagram](https://matplotlib.org/examples/showcase/anatomy.html)
[Matplotlib tutorial](https://matplotlib.org/tutorials/introductory/pyplot.html#sphx-glr-tutorials-introductory-pyplot-py)
