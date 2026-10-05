# Simple Linear Regression — Closed-Form Solution

## Problem

Implement a function `fit_line(x, y)` that fits a straight line to the given data using the **closed-form solution of simple linear regression**.

The fitted line is

$$
\hat{y}=wx+b
$$

where:

* \(w\) is the slope
* \(b\) is the intercept
* \(x\) is the input feature
* \(y\) is the observed target
* \(\hat y\) is the predicted value

The required formulas are

$$
w=
\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}
{\sum_{i=1}^{n}(x_i-\bar{x})^2}
$$

and

$$
b=\bar{y}-w\bar{x}
$$

If all \(x_i\) values are identical, the denominator becomes zero. In that case, the problem specifies returning

$$
(w,b)=(0,\bar y)
$$

---

# 1. Intuition Behind Linear Regression

Suppose we have \(n\) observations:

$$
(x_1,y_1),(x_2,y_2),\ldots,(x_n,y_n)
$$

We want to find the straight line

$$
\hat y=wx+b
$$

that best represents these points.

For every observation \(i\), the model predicts

$$
\hat y_i=wx_i+b
$$

The difference between the actual value and prediction is called the **residual**:

$$
e_i=y_i-\hat y_i
$$

Therefore,

$$
e_i=y_i-(wx_i+b)
$$

A natural objective would be to minimize the residuals. However, positive and negative residuals could cancel each other.

For example,

$$
(+5)+(-5)=0
$$

even though both predictions are wrong.

Therefore, ordinary least squares minimizes the **sum of squared residuals**:

$$
J(w,b)=\sum_{i=1}^{n}(y_i-wx_i-b)^2
$$

This is the least-squares objective function.

---

# 2. Deriving the Slope and Intercept

We need to find \(w\) and \(b\) that minimize

$$
J(w,b)=\sum_{i=1}^{n}(y_i-wx_i-b)^2
$$

Since \(J\) is a differentiable quadratic function of \(w\) and \(b\), its minimum can be found by setting its partial derivatives equal to zero.

Thus,

$$
\frac{\partial J}{\partial w}=0
$$

and

$$
\frac{\partial J}{\partial b}=0
$$

---

# 3. Deriving the Intercept

Start with

$$
J(w,b)=\sum_{i=1}^{n}(y_i-wx_i-b)^2
$$

Differentiate with respect to \(b\):

$$
\frac{\partial J}{\partial b}
=
\sum_{i=1}^{n}
2(y_i-wx_i-b)(-1)
$$

Therefore,

$$
\frac{\partial J}{\partial b}
=
-2\sum_{i=1}^{n}(y_i-wx_i-b)
$$

At the minimum:

$$
-2\sum_{i=1}^{n}(y_i-wx_i-b)=0
$$

Divide by \(-2\):

$$
\sum_{i=1}^{n}(y_i-wx_i-b)=0
$$

Expand the summation:

$$
\sum_{i=1}^{n}y_i
-
w\sum_{i=1}^{n}x_i
-
\sum_{i=1}^{n}b
=0
$$

Since \(b\) is constant,

$$
\sum_{i=1}^{n}b=nb
$$

Therefore,

$$
\sum y_i-w\sum x_i-nb=0
$$

Rearrange:

$$
nb=\sum y_i-w\sum x_i
$$

Divide by \(n\):

$$
b=
\frac{\sum y_i}{n}
-
w\frac{\sum x_i}{n}
$$

Using the definitions

$$
\bar{x}=\frac{1}{n}\sum x_i
$$

and

$$
\bar{y}=\frac{1}{n}\sum y_i
$$

we obtain

$$
\boxed{b=\bar y-w\bar x}
$$

This is the intercept formula used by the implementation.

---

# 4. Deriving the Slope

Now differentiate the objective function with respect to \(w\):

$$
J(w,b)=\sum_{i=1}^{n}(y_i-wx_i-b)^2
$$

Using the chain rule:

$$
\frac{\partial J}{\partial w}
=
-2\sum_{i=1}^{n}x_i(y_i-wx_i-b)
$$

At the minimum:

$$
-2\sum_{i=1}^{n}x_i(y_i-wx_i-b)=0
$$

Therefore,

$$
\sum_{i=1}^{n}x_i(y_i-wx_i-b)=0
$$

Expand:

$$
\sum x_iy_i
-
w\sum x_i^2
-
b\sum x_i
=0
$$

Thus,

$$
\sum x_iy_i
=
w\sum x_i^2+b\sum x_i
$$

Now substitute

$$
b=\bar y-w\bar x
$$

into the equation:

$$
\sum x_iy_i
=
w\sum x_i^2
+
(\bar y-w\bar x)\sum x_i
$$

Since

$$
\sum x_i=n\bar x
$$

we get

$$
\sum x_iy_i
=
w\sum x_i^2
+
n\bar x\bar y
-
wn\bar x^2
$$

Rearrange the terms containing \(w\):

$$
\sum x_iy_i-n\bar x\bar y
=
w
\left(
\sum x_i^2-n\bar x^2
\right)
$$

Therefore,

$$
w=
\frac{
\sum x_iy_i-n\bar x\bar y
}{
\sum x_i^2-n\bar x^2
}
$$

This is an equivalent form of the slope formula.

---

# 5. Converting the Slope to the Centered Form

The implementation uses the more numerically meaningful centered form:

$$
\boxed{
w=
\frac{
\sum (x_i-\bar x)(y_i-\bar y)
}{
\sum (x_i-\bar x)^2
}
}
$$

Let's verify why this is equivalent.

Consider the numerator:

$$
\sum (x_i-\bar x)(y_i-\bar y)
$$

Expand:

$$
=
\sum
(x_iy_i-x_i\bar y-\bar xy_i+\bar x\bar y)
$$

Therefore,

$$
=
\sum x_iy_i
-\bar y\sum x_i
-\bar x\sum y_i
+\sum\bar x\bar y
$$

Using

$$
\sum x_i=n\bar x
$$

and

$$
\sum y_i=n\bar y
$$

we obtain

$$
=
\sum x_iy_i
-n\bar x\bar y
-n\bar x\bar y
+n\bar x\bar y
$$

Hence,

$$
\boxed{
\sum (x_i-\bar x)(y_i-\bar y)
=
\sum x_iy_i-n\bar x\bar y
}
$$

Now consider the denominator:

$$
\sum(x_i-\bar x)^2
$$

Expand:

$$
\sum(x_i^2-2x_i\bar x+\bar x^2)
$$

Therefore,

$$
=
\sum x_i^2
-2\bar x\sum x_i
+\sum\bar x^2
$$

Using

$$
\sum x_i=n\bar x
$$

we obtain

$$
=
\sum x_i^2
-2n\bar x^2
+n\bar x^2
$$

Therefore,

$$
\boxed{
\sum(x_i-\bar x)^2
=
\sum x_i^2-n\bar x^2
}
$$

Substituting these two identities gives

$$
\boxed{
w=
\frac{
\sum(x_i-\bar x)(y_i-\bar y)
}{
\sum(x_i-\bar x)^2
}
}
$$

---

# 6. Connection to Covariance and Variance

The numerator resembles covariance:

$$
\operatorname{Cov}(x,y)
=
\frac{1}{n}
\sum_{i=1}^{n}
(x_i-\bar x)(y_i-\bar y)
$$

and the denominator resembles variance:

$$
\operatorname{Var}(x)
=
\frac{1}{n}
\sum_{i=1}^{n}
(x_i-\bar x)^2
$$

Therefore,

$$
w=
\frac{n\operatorname{Cov}(x,y)}
{n\operatorname{Var}(x)}
$$

and the \(n\) terms cancel:

$$
\boxed{
w=\frac{\operatorname{Cov}(x,y)}
{\operatorname{Var}(x)}
}
$$

This explains the comment in the original code:

> covariance/variance closed form

The slope tells us how strongly \(y\) changes with \(x\), normalized by the amount of variation present in \(x\).

---

# 7. Why the Denominator Can Become Zero

The denominator is

$$
\sum(x_i-\bar x)^2
$$

Every term is non-negative because it is squared.

Therefore,

$$
\sum(x_i-\bar x)^2=0
$$

can happen only when every term is zero:

$$
x_i-\bar x=0
$$

for every \(i\).

Hence,

$$
x_1=x_2=\cdots=x_n=\bar x
$$

In other words, **all input values are identical**.

For example:

$$
x=[5,5,5,5]
$$

Then

$$
\bar x=5
$$

and

$$
x-\bar x=[0,0,0,0]
$$

so

$$
\sum(x_i-\bar x)^2=0
$$

The slope would require division by zero and is therefore undefined.

The problem explicitly specifies the fallback:

$$
\boxed{w=0,\qquad b=\bar y}
$$

which corresponds to returning:

```python
(0.0, mean_y)
```

---

# 8. NumPy Implementation

```python
import numpy as np


def fit_line(x: np.ndarray, y: np.ndarray) -> tuple[float, float]:
    """
    Simple linear regression by the covariance/variance closed form.

    x, y: shape (n,).

    w = sum((x-mean_x)*(y-mean_y)) / sum((x-mean_x)^2)
    b = mean_y - w * mean_x

    If every x_i is identical, the denominator is 0: return (0.0, mean_y)
    instead of dividing.
    """

    mean_x = np.mean(x)
    mean_y = np.mean(y)

    numerator = np.sum((x - mean_x) * (y - mean_y))
    denominator = np.sum((x - mean_x) ** 2)

    if denominator == 0:
        return (0.0, mean_y)

    w = numerator / denominator
    b = mean_y - w * mean_x

    return (w, b)
```

---

# 9. Mapping Mathematics to Code

| Mathematical expression            | Python implementation                 |
| ---------------------------------- | ------------------------------------- |
| \(\bar{x}\)                        | `np.mean(x)`                          |
| \(\bar{y}\)                        | `np.mean(y)`                          |
| \(x_i-\bar{x}\)                    | `x - mean_x`                          |
| \(y_i-\bar{y}\)                    | `y - mean_y`                          |
| \((x_i-\bar{x})(y_i-\bar{y})\)     | `(x - mean_x) * (y - mean_y)`         |
| \(\sum(x_i-\bar{x})(y_i-\bar{y})\) | `np.sum((x - mean_x) * (y - mean_y))` |
| \((x_i-\bar{x})^2\)                | `(x - mean_x) ** 2`                   |
| \(\sum(x_i-\bar{x})^2\)            | `np.sum((x - mean_x) ** 2)`           |
| \(w\)                              | `numerator / denominator`             |
| \(b=\bar y-w\bar x\)               | `mean_y - w * mean_x`                 |

---

# 10. Complete Numerical Example

Consider

$$
x=[1,2,3]
$$

and

$$
y=[3,5,7]
$$

### Step 1 — Means

$$
\bar x=\frac{1+2+3}{3}=2
$$

$$
\bar y=\frac{3+5+7}{3}=5
$$

### Step 2 — Center the data

$$
x-\bar x=[-1,0,1]
$$

$$
y-\bar y=[-2,0,2]
$$

### Step 3 — Numerator

$$
\sum(x_i-\bar x)(y_i-\bar y)
$$

$$
=(-1)(-2)+(0)(0)+(1)(2)
$$

$$
=2+0+2
$$

$$
=4
$$

### Step 4 — Denominator

$$
\sum(x_i-\bar x)^2
$$

$$
=(-1)^2+0^2+1^2
$$

$$
=1+0+1
$$

$$
=2
$$

### Step 5 — Slope

$$
w=\frac{4}{2}=2
$$

### Step 6 — Intercept

$$
b=\bar y-w\bar x
$$

$$
b=5-(2)(2)
$$

$$
b=1
$$

Therefore,

$$
\boxed{w=2,\quad b=1}
$$

and the fitted line is

$$
\boxed{\hat y=2x+1}
$$

---

# 11. Vectorization

An important implementation detail is that the solution uses **NumPy vectorization**.

For example:

```python
(x - mean_x) * (y - mean_y)
```

performs element-wise operations on the entire arrays.

It is conceptually equivalent to:

```python
numerator = 0

for i in range(len(x)):
    numerator += (x[i] - mean_x) * (y[i] - mean_y)
```

Similarly,

```python
np.sum((x - mean_x) ** 2)
```

is conceptually equivalent to:

```python
denominator = 0

for i in range(len(x)):
    denominator += (x[i] - mean_x) ** 2
```

The NumPy version is shorter, idiomatic for numerical Python, and delegates the array operations to optimized native implementations.

---

# 12. Complexity Analysis

Let \(n\) be the number of observations.

### Time Complexity

Computing the means requires traversing the arrays:

$$
O(n)
$$

Computing the numerator:

$$
O(n)
$$

Computing the denominator:

$$
O(n)
$$

Therefore, the total time complexity is:

$$
\boxed{O(n)}
$$

### Auxiliary Space

The vectorized NumPy expressions create temporary arrays such as

$$
x-\bar x
$$

and

$$
y-\bar y
$$

Therefore, the implementation uses:

$$
\boxed{O(n)}
$$

temporary memory in addition to the input arrays.

This is different from a hand-written scalar loop, which could compute the sums using \(O(1)\) auxiliary scalar memory.

---

# 13. Important Numerical Consideration

The centered formulation

$$
w=
\frac{
\sum(x_i-\bar x)(y_i-\bar y)
}{
\sum(x_i-\bar x)^2
}
$$

is preferable conceptually to directly computing

$$
w=
\frac{
\sum x_iy_i-n\bar x\bar y
}{
\sum x_i^2-n\bar x^2
}
$$

because the latter involves subtracting potentially large, nearly equal numbers.

For example, if \(x\) contains very large values, both

$$
\sum x_i^2
$$

and

$$
n\bar x^2
$$

may be extremely large while their difference is relatively small. Floating-point arithmetic can lose precision in such subtraction.

Centering the data first generally gives a more numerically stable formulation.

For a production-grade regression implementation, numerical conditioning and floating-point precision should be considered carefully, especially when feature magnitudes are large or the variance of \(x\) is very small.

---

# 14. Final Result

The function implements ordinary least-squares simple linear regression:

$$
\boxed{\hat y=wx+b}
$$

with

$$
\boxed{
w=
\frac{
\sum_{i=1}^{n}(x_i-\bar x)(y_i-\bar y)
}{
\sum_{i=1}^{n}(x_i-\bar x)^2
}
}
$$

and

$$
\boxed{
b=\bar y-w\bar x
}
$$

The derivation comes directly from minimizing the squared-error objective

$$
\boxed{
J(w,b)=\sum_{i=1}^{n}(y_i-wx_i-b)^2
}
$$

with respect to \(w\) and \(b\).

The implementation also explicitly handles the degenerate case where

$$
\operatorname{Var}(x)=0
$$

by returning

$$
\boxed{(0,\bar y)}
$$

as required by the problem.
