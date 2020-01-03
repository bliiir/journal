The Hundred-page Machine Learning Book

Chapter 1

## 2 Notation and Definitions

### 2.1 Notation

#### 2.1.1 Data Structures
![](https://www.dropbox.com/s/gwjfis5ptcmvr66/Screenshot%202020-01-02%2018.18.21.png?dl=1)

| Term | Definition | notation | book | Python |
| :-- | :-- | :-- | :-- | :-- | :-- |
| *scalar* | number | lowercase italic| $\mathit{x} = 15$ | `x = 15` |
| *vector* | list of scalars | lowercase bold | $\mathbf{a} = [\ 2,\ 3\ ]$ | `a = [2,3]` or `a = list(2,3)` |
| *dimension* | number of elements in a vector | superscript lowercase italic in parenthesis  | $a^{(j)}$ | `j = len(a)`  |
| *position* | position of an attribute in a vector | superscript lowercase italic in parenthesis  | $a^{(1)} \rightarrow 2$| `a[0] == 2`  |
| *matrix* | multidimensional array | upppercase bold | $\mathbf{W} = \begin{bmatrix}2 & 4 & -3 \\21 & -6 & -1\end{bmatrix}$ | `W = [ [2, 4, -3], [21, -6, -1] ]` or `numpy.array( [2, 4, -3], [21, -6, -1] )` |
| *set* | unordered list of scalars | caligraphic uppercase | $\mathcal{S} = \{1, 3, 18, 23, 235\}$ | `S = set(1, 3, 18, 23, 235)` |

![]()

##### Sets
| Term | book | Python |
| :-- | :-- | :-- |
| *belongs* | $\mathit{x} \in \mathcal{S}$ | Boolean check `x in S`, Add x to set `S.add(x)` |
| *intersection* | $\mathcal{S_3} \leftarrow \mathcal{S_1} \cap \mathcal{S_2} $ | `S3 = S1.intersection(S2)` |
| *union* | $\mathcal{S_3} \leftarrow \mathcal{S_1} \cup \mathcal{S_2} $ | `S3 = S1.union(S2)` |

---

#### 2.1.2 Capital Sigma Notation
| Term | Definition | book | Python |
| :-- | :-- | :-- | :-- |
| *Capital Sigma* | The summation of an array of scalars | $\sum_{i=1}^n x_i = x_1 + x_2 + ... + x_{n-1} + x_n$ | `sum(x1, x2 ... xn)` or `numpy.sum(x1, x2 ... xn)` |

---

#### 2.1.3 Capital Pi Notation
| Term | Definition | book | Python |
| :-- | :-- | :-- | :-- |
| *Capital Pi* | The product of an array of scalars | $\prod_{i=1}^n x_i = x_1 + x_2 + ... + x_{n-1} + x_n$ | `numpy.prod(x1, x2 ... xn)` |

#### 2.1.4 Operations on Sets
| Term | Definition | book | Python |
| :-- | :-- | :-- | :-- |
| *Derived set creation operator* | create a new set $\mathcal{S}'$ from $\mathcal{S}$ | $S' \leftarrow \{x^2 \vert x \in \mathcal{S}, x > 3\}$  | `[x for x in S if x>3 ]` |

---

#### 2.1.5 Operations on Vectors
Given:
$x = [ 1, 2, 3 ]$

$y = 2$

$z = [ 4, 5, 6 ]$

$u = [ 1, 2 ]$


$\mathbf{W} = \begin{bmatrix}w^{(1,1)} & w^{(1,2)} & w^{(1,3)} \\w^{(2,1)} & w^{(2,2)} & w^{(2,3)}\end{bmatrix} = \begin{bmatrix}2 & 4 & -3 \\21 & -6 & -1\end{bmatrix}$



##### The sum of two vectors is a vector:
$x + z = [x^{(1)} + z^{(1)}, x^{(2)} + z^{(2)}, x^{(3)} + z^{(3)}]$
$x + z = [1 + 4, 2 + 5, 3 + 6]$
$x + z = [5, 7, 9]$

##### The difference of two vectors is a vector:
$x - z = [x^{(1)} - z^{(1)}, x^{(2)} - z^{(2)}, x^{(3)} - z^{(3)}]$
$x - z = [1 - 4, 2 - 5, 3 - 6]$
$x - z = [-3, -3, -3]$

##### The product of a vector and a scalar is a vector:
$x \times z = [x^{(1)} \times y, x^{(2)} \times y, x^{(3)} \times y]$
$x - z = [1 \times 2, 2 \times 2, 3 \times 2]$
$x - z = [2, 4, 6]$

##### The dot-product of two vectors is a scalar:
$xz = x \cdot z \large{/} \small \sum_{i=1}^{3}x^{i}z^{i}$
$xz = x^1 \cdot z^1 + x^2 \cdot z^2 + x^3 \cdot z^3$
$xz = 1 \cdot 4 + 2 \cdot 5 + 3 \cdot 6$
$xz = 4 + 10 + 18$
$xz = 32$

##### The multiplication of a matrix $\mathbf{W}$ with a vector $\mathbf{x}$ is a vector:

$\mathbf{W}\mathbf{x} = \begin{bmatrix}w^{(1,1)} & w^{(1,2)} & w^{(1,3)} \\w^{(2,1)} & w^{(2,2)} & w^{(2,3)}\end{bmatrix} \begin{bmatrix} x^{(1)} \\x^{(2)} \\x^{(3)} \end{bmatrix}$

$\mathbf{W}\mathbf{x} = \begin{bmatrix}2 & 4 & -3 \\21 & -6 & -1\end{bmatrix} \begin{bmatrix} 1 \\2 \\3 \end{bmatrix}$

$\mathbf{W}\mathbf{x} = \begin{bmatrix}2 \times 1 + 4 \times 2 + -3 \times 3\\21 \times 1 + -6 \times 2 + -1 \times 3\end{bmatrix} $

$\mathbf{W}\mathbf{x} = \begin{bmatrix}2 + 8 + -9\\21 + -12 + -3\end{bmatrix} $

$\mathbf{W}\mathbf{x} = \begin{bmatrix}1\\30\end{bmatrix}$

##### The multiplication of a vector $\mathbf{u}$ with a matrix $\mathbf{W}$ is a vector:

$\mathbf{u}\mathbf{W} = \begin{bmatrix} x^{(1)} & x^{(2)} \end{bmatrix} \begin{bmatrix}w^{(1,1)} & w^{(1,2)} & w^{(1,3)} \\w^{(2,1)} & w^{(2,2)} & w^{(2,3)}\end{bmatrix}$

$\mathbf{u}\mathbf{W} = \begin{bmatrix} 1 & 2 \end{bmatrix} \begin{bmatrix}2 & 4 & -3 \\21 & -6 & -1\end{bmatrix}$

$\mathbf{u}\mathbf{W} = \begin{bmatrix}2 \times 1 + 21 \times 2, 4 \times 1 + -6 \times 2,  -3 \times 1 + -1 \times 2 \end{bmatrix}$

$\mathbf{u}\mathbf{W} = \begin{bmatrix}44, -8,  -5 \end{bmatrix}$

---

#### 2.1.6 Functions
| Term | Definition | book | Python |
| :-- | :-- | :-- | :-- |
| *function* | A relation that associates each element, $x$, of a set $X$ to a single element, $y$, of the set $Y$ | $y = f(x)$, or  $Y^{(n)} = f(X^{(n)})$ | `y = my_func(x)`, or `Y[n] = my_func(X[n])` |
| *domain* | The set of $x$ elements | $X = [x^1, x^2, ... x^{n-1}, x^n]$ | `X = [x_1, x_2, ... x_1-n, x_n`|
| *co-domain* | The set of $y$ elements  | $Y = [y^1, y^2, ... y^{n-1}, y^n]$ | `Y = [y_1, y_2, ... y_1-n, y_n` |
| *interval* | a set of real numbers that lies between and includes two numbers in a set | $[0,1]$ | assuming 0.2 increments ~ `interval = [0, 0.2, 0.4, 0.6, 0.8, 1.0]` |
| *open interval* | a set of real numbers that lies between but does not include two numbers in a set | $(0,1)$ | assuming 0.2 increments ~ `open_interval = [0.2, 0.4, 0.6, 0.8]`
| *local minimum* | $f(x)$ has a local minimum at x = c if $f(x) \leq f(c)$ for every $x$ in some open interval around $x = c$ | $local\ minimum = min_{a \in \mathcal{A_{interval}}} f(a)$ | `local_minima.append(min([my_func(x) for x in open_interval]))`
| *global minimum* | The minimal value among all the local minima | $global\ minimum = min_{a \in \mathcal{A}} f(a)$ | `global_minimum = min(local_minima)`|

![](https://www.dropbox.com/s/j8dy4zzwm8nwk8c/Screenshot%202020-01-02%2018.17.33.png?dl=1)

---

#### 2.17 Max and Arg Max


Given:
$f(x) = 4x^2 + 3x + 2$
$\mathcal{A} = \{1, 2, 5, 4\}$
$\mathcal{f(A)} = \{1, 2, 5, 4\}$

```py
f = lambda x: 4*x**x + 3*x + 2
X = [1,2,5,4]
Y = [f(x) for x in X]

max_ix = Y.index(max(Y))
maxY = Y[max_ix]
argmax = X[max_ix]

print(maxY)
print(argmax)
```
```shell
12517
5
```


$max_{a \in \mathcal{A}}\ f(a) = 12517$
$arg\ max_{a \in \mathcal{A}}\ f(a) = 5$

---

#### 2.1.8
| Term | Definition | book | Python |
| :-- | :-- | :-- | :-- |
| *assignment operator* | assigns a value to a variable | $a \leftarrow f(x)$ | `a = my_func(x)` |

---

#### 2.1.9 Derivative and gradient

##### derivative
The derivative $f'$ describes how fast a function $f$ grows.
$f'$ is the slope of $f$
differentiation is the process of finding a derivative

$f(x) = ax^3 + bx^2 + cx^1 + dx^0$
$f'(x) = 3ax + 2b + 1c + 0d$

##### chain rule
Use the chain rule to find the derivative of non-basic functions

$\begin{aligned}
F(x) &= f(g(x)) \\
F'(x) &= f'(g(x)) \cdot g'(x)
\end{aligned}$

###### Example:

$\begin{aligned}
Given:\\\\
F(x) &= (5x + 1)^2\\
\\
Then:\\
\\
g(x) &= 5x + 1\\
g'(x) &= 5 \\
\\
f(x) &= (g(x))^2 \\
f'(x) &= 2(g(x)) \\
\\
F'(x) &= f'(g(x)) \cdot g'(x) \\
F'(x) &= 2(5x + 1) \cdot 5 \\
F'(x) &= 10(5x + 1)\\
F'(x) &= 50x + 10
\end{aligned}$

##### partial derivatives
${∂f} \over {∂x^{(1)}}$

The act of finding the derivative by focusing on one of the functions inputs

$\begin{aligned}
f([x^{(1)}, x^{(2)}]) &= ax^{(1)} + bx^{(2)} + c\\
\\
{∂f} \over {∂x^{(1)}} &= a + 0 + 0 \\
\\
{∂f} \over {∂x^{(1)}} &= a \\
\\\\
{∂f} \over {∂x^{(2)}} &= 0 + b + 0\\
\\
{∂f} \over {∂x^{(2)}} &= b
\end{aligned}$

##### gradient
A vector of partial derivatives

---

#### 2.2 Random variable
![](https://www.dropbox.com/s/r64ebhye0f4wsn0/Screenshot%202020-01-03%2015.41.10.png?dl=1)

| Term | Definition | notation | book | Python |
| :-- | :-- | :-- | :-- | :-- |
| *random variable* | numerical value that is the outcome of a random phenomenonm | uppercase italic |$\mathcal{X}$ | `X` |
|  *discrete random variable* | random variable with only a countable number of discrete values | - |example $[1, 2, 3,\ 4]$, $[red,\ yellow,\ blues]$ | `random.randint(1,4)`, `random.choice[red, green, blue]` |
| *probability mass function* | The probability of the discrete random variable | - | $\begin{aligned} pmf:~ {Pr}(\mathit{X = red}) &= 0.3\\ {Pr}(\mathit{X = yellow}) &= 0.45\\ {Pr}(\mathit{X = blue}) &= 0.25 \end{aligned}$ | `random.choices(["red", "yellow", "blue"], [0.3, 0.45, 0.25])` |
| *continuous random variable* | non-discrete random variable from an infinite number of variables in an interval | - | $CRV$ | - |
| *probability density function* | describes the probability distribution of a $CRV$ | - | $pdf$ | - |
| *probability distribution* | $pmf$ for discreete variables and $pdf$ for continuous variables |
| [*expectation*](https://en.wikipedia.org/wiki/Mean) | The expected value, aka **mean** or **average** of $X$  | | $\mathbb{E[X]}$ or $\mu$ |
| |  for discrete random variable | |$\begin{aligned} \mathbb{E[X]} = \sum_{i=1}^k [x_i \cdot Pr(X = x_i)] \end{aligned}$ | `E = mean(X)`, or `numpy.mean(X)` |
| |  for continuous random variable | |$\begin{aligned} \mathbb{E[X]} = \int_{\mathbb{R}}~x f_X(x)dx \end{aligned}$ | |
| [*standard deviation*](https://en.wikipedia.org/wiki/Standard_deviation) | The square root of the variance | sigma | $\begin{aligned} \sigma = \sqrt{\mathbb{E}[X-\mu]^2} \end{aligned}$ | `statistics.stdev(X)`, or `numpy.var(X)` |
|  |  | discrete | $\begin{aligned} \tiny{\sigma = \sqrt{Pr(X=x_1)(x_1-\mu)^2 + Pr(X=x_2)(x_2-\mu)^2 + ... + Pr(X=x_k)(x_k-\mu)^2}} \end{aligned}$ | `statistics.stdev(X)`, or `numpy.var(X)` |
| [*variance*](https://en.wikipedia.org/wiki/Variance) | measures how far a set of numbers are spread out from their average value | sigma | $\sigma^2 = \mathbb{E}[X-\mu]^2$ |`statistics.variance(X)`, or `numpy.std(X)` |
| *integral* | the signed area of the graph | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9f/Integral_example.svg/300px-Integral_example.svg.png) | $\begin{aligned} \mathbb{E[X]} = \int_a^bf(x)dx \end{aligned}$ | [`numpy.trapz(X)`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.trapz.html)

#### 2.3 Unbiased estimators
| Term | Definition | notation | book | Python |
| :-- | :-- | :-- | :-- | :-- |
| *sample statistic* | | | $\hat{\theta}$ | |
| *sample statistic* | | | $\hat{\theta}$ | |
