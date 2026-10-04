# The Click-Rate Band

**Difficulty:** Easy<br>
**Category:** Probability & Statistics<br>
**Language:** Python

---

## 1. Problem Overview

A search-ads team wants to report its **click-through rate (CTR)** every day.

Suppose an advertisement is shown to `n` users, and `clicks` users click on it.

The simplest thing we can report is:

$$
\text{CTR} = \frac{\text{clicks}}{n}
$$

This is called a **point estimate**.

However, a point estimate alone does not tell us how reliable the estimate is.

For example:

* 2 clicks out of 4 impressions → CTR = 50%
* 500,000 clicks out of 1,000,000 impressions → CTR = 50%

Both have exactly the same observed CTR:

$$
0.5 = 50\%
$$

But the second estimate is much more reliable because it is based on a much larger sample.

Therefore, this problem asks us to calculate a **95% confidence interval** around the observed click rate.

---

# 2. Important Terms

## 2.1 Sample Size (`n`)

`n` is the total number of observations.

In this problem, it represents the total number of times the advertisement was shown.

For example:

```text
n = 1000
```

means the advertisement was shown 1000 times.

---

## 2.2 Successes (`clicks`)

`clicks` represents the number of successful events.

Here, a "success" means that a user clicked the advertisement.

For example:

```text
clicks = 45
```

means 45 out of 1000 users clicked.

---

## 2.3 Point Estimate (`p_hat`)

The observed click rate is:

$$
\hat p = \frac{\text{clicks}}{n}
$$

The symbol `p_hat` is written mathematically as:

$$
\hat p
$$

and is called the **sample proportion** or **estimated probability of success**.

For:

$$
n=1000
$$

and

$$
clicks=45
$$

we get:

$$
\hat p=\frac{45}{1000}=0.045
$$

Therefore:

$$
\boxed{\hat p=0.045}
$$

or:

$$
\boxed{4.5\%}
$$

---

# 3. Why Do We Need a Confidence Interval?

Suppose we observe:

$$
\hat p=0.045
$$

Can we say that the true CTR is exactly 4.5%?

No.

The 4.5% is calculated from a **sample**.

If we repeated the experiment, we might get:

```text
Experiment 1 → 4.5%
Experiment 2 → 4.8%
Experiment 3 → 4.2%
Experiment 4 → 4.6%
```

The observed proportion changes from sample to sample.

This variation is called **sampling variability**.

Therefore, instead of reporting only:

$$
\hat p=0.045
$$

we report a range:

$$
\boxed{\text{lower} \leq p \leq \text{upper}}
$$

This range is our **confidence interval**.

---

# 4. Standard Error

The first quantity we need is the **Standard Error (SE)**.

The standard error measures the expected amount of sampling variation in our estimate.

For a sample proportion:

$$
\boxed{
SE=\sqrt{\frac{\hat p(1-\hat p)}{n}}
}
$$

where:

* \(\hat p\) = observed proportion
* \(n\) = sample size
* \(SE\) = standard error

---

## 4.1 Intuition Behind Standard Error

Consider two experiments.

### Experiment A

```text
10 impressions
2 clicks
```

$$
\hat p=0.2
$$

### Experiment B

```text
10,000 impressions
2,000 clicks
```

$$
\hat p=0.2
$$

Both have the same CTR.

But Experiment B has much more data.

Because `n` appears in the denominator:

$$
SE=\sqrt{\frac{\hat p(1-\hat p)}{n}}
$$

a larger `n` produces a smaller standard error.

Therefore:

```text
Small sample
     ↓
Large uncertainty
     ↓
Large SE
     ↓
Wide confidence interval
```

while:

```text
Large sample
     ↓
Small uncertainty
     ↓
Small SE
     ↓
Narrow confidence interval
```

---

# 5. Where Does the Standard Error Formula Come From?

The problem gives:

$$
SE=\sqrt{\frac{\hat p(1-\hat p)}{n}}
$$

But it is useful to understand why this formula exists.

Suppose every advertisement impression can be represented as a **Bernoulli random variable**:

$$
X=
\begin{cases}
1 & \text{if the user clicks}\\
0 & \text{if the user does not click}
\end{cases}
$$

Let the true probability of a click be:

$$
p
$$

For a Bernoulli random variable:

$$
E[X]=p
$$

and:

$$
Var(X)=p(1-p)
$$

Now suppose we have `n` independent observations:

$$
X_1,X_2,\ldots,X_n
$$

The sample proportion is:

$$
\hat p=\frac{X_1+X_2+\cdots+X_n}{n}
$$

The variance of the sample proportion is:

$$
Var(\hat p)=\frac{p(1-p)}{n}
$$

Therefore, its standard deviation is:

$$
SD(\hat p)
=
\sqrt{\frac{p(1-p)}{n}}
$$

Since the true value \(p\) is unknown, we estimate it using \(\hat p\):

$$
\boxed{
SE=
\sqrt{\frac{\hat p(1-\hat p)}{n}}
}
$$

This is the standard error used by the problem.

---

# 6. What Does `z = 1.959964` Mean?

The problem specifies:

$$
z=1.959964
$$

This is the critical value used for an approximately **95% two-sided normal interval**.

For a standard normal random variable:

$$
Z\sim N(0,1)
$$

approximately 95% of the distribution lies between:

$$
-1.96
$$

and:

$$
+1.96
$$

Visually:

```text
             approximately 95%
        <------------------------>
                │
                │
       -1.96    0    +1.96
         │      │       │
---------|------|-------|---------
```

The exact value supplied by the problem is:

$$
1.959964
$$

We use that value directly rather than calculating it at runtime.

---

# 7. Deriving the Confidence Interval

The general form of a normal confidence interval is:

$$
\text{estimate}
\pm
\text{critical value}\times\text{standard error}
$$

For this problem:

$$
\text{estimate}=\hat p
$$

$$
\text{critical value}=z
$$

$$
\text{standard error}=SE
$$

Therefore:

$$
\boxed{
\hat p\pm zSE
}
$$

This gives two boundaries.

### Lower bound

$$
\boxed{
lower=\hat p-zSE
}
$$

### Upper bound

$$
\boxed{
upper=\hat p+zSE
}
$$

So the complete interval is:

$$
\boxed{
\left[
\hat p-zSE,\;
\hat p+zSE
\right]
}
$$

---

# 8. Complete Mathematical Formula

The entire problem can therefore be solved using four calculations.

### Step 1 — Point estimate

$$
\boxed{
\hat p=\frac{clicks}{n}
}
$$

### Step 2 — Standard error

$$
\boxed{
SE=
\sqrt{\frac{\hat p(1-\hat p)}{n}}
}
$$

### Step 3 — Lower bound

$$
\boxed{
lower=\hat p-1.959964\times SE
}
$$

### Step 4 — Upper bound

$$
\boxed{
upper=\hat p+1.959964\times SE
}
$$

---

# 9. Worked Example

Consider:

```text
n = 1000
clicks = 45
```

## Step 1: Calculate the click rate

$$
\hat p=\frac{45}{1000}
$$

$$
\hat p=0.045
$$

So:

$$
\boxed{\hat p=0.045}
$$

---

## Step 2: Calculate the Standard Error

$$
SE=
\sqrt{
\frac{0.045(1-0.045)}
{1000}
}
$$

First:

$$
1-0.045=0.955
$$

Therefore:

$$
SE=
\sqrt{
\frac{0.045\times0.955}{1000}
}
$$

$$
SE\approx0.006556
$$

---

## Step 3: Calculate the Lower Bound

$$
lower
=
0.045-(1.959964)(0.006556)
$$

$$
lower\approx0.032151
$$

---

## Step 4: Calculate the Upper Bound

$$
upper
=
0.045+(1.959964)(0.006556)
$$

$$
upper\approx0.057849
$$

Therefore:

$$
\boxed{
[0.032151,\;0.057849]
}
$$

or approximately:

```text
3.2151% to 5.7849%
```

---

# 10. Understanding the Result

The output is:

```text
0.045000 0.032151 0.057849
```

The three values mean:

```text
0.045000
   ↓
Observed click rate
   ↓
4.5%
```

```text
0.032151
   ↓
Lower confidence bound
   ↓
3.2151%
```

```text
0.057849
   ↓
Upper confidence bound
   ↓
5.7849%
```

So the point estimate is:

$$
4.5\%
$$

and the calculated 95% confidence interval is approximately:

$$
[3.2151\%,5.7849\%]
$$

---

# 11. Algorithm

The algorithm is very simple.

```text
Read n and clicks

Calculate:
    p_hat = clicks / n

Calculate:
    SE = sqrt(p_hat * (1 - p_hat) / n)

Calculate:
    lower = p_hat - 1.959964 * SE

Calculate:
    upper = p_hat + 1.959964 * SE

Print p_hat, lower, upper
```

---

# 12. Python Implementation

```python
import math

Z_95 = 1.959964


def click_rate_band(n: int, clicks: int) -> tuple[float, float, float]:
    p_hat = clicks / n

    SE = math.sqrt(p_hat * (1 - p_hat) / n)

    lower = p_hat - Z_95 * SE
    upper = p_hat + Z_95 * SE

    return p_hat, lower, upper


n, clicks = map(int, input().split())

p_hat, lower, upper = click_rate_band(n, clicks)

print(f"{p_hat:.6f} {lower:.6f} {upper:.6f}")
```

---

# 13. Code Explanation

## Import `math`

```python
import math
```

The `math` module provides mathematical functions such as:

```python
math.sqrt()
```

which calculates square roots.

---

## Store the Z value

```python
Z_95 = 1.959964
```

This stores the 95% normal critical value specified by the problem.

---

## Define the function

```python
def click_rate_band(n: int, clicks: int) -> tuple[float, float, float]:
```

The function receives:

* `n` → total number of impressions
* `clicks` → number of clicks

and returns three floating-point values:

```text
p_hat
lower
upper
```

---

## Calculate the point estimate

```python
p_hat = clicks / n
```

This implements:

$$
\hat p=\frac{clicks}{n}
$$

---

## Calculate standard error

```python
SE = math.sqrt(p_hat * (1 - p_hat) / n)
```

This implements:

$$
SE=
\sqrt{
\frac{\hat p(1-\hat p)}
{n}
}
$$

---

## Calculate lower bound

```python
lower = p_hat - Z_95 * SE
```

This implements:

$$
lower=\hat p-zSE
$$

---

## Calculate upper bound

```python
upper = p_hat + Z_95 * SE
```

This implements:

$$
upper=\hat p+zSE
$$

---

## Return the results

```python
return p_hat, lower, upper
```

The function returns the three calculated values.

---

# 14. Reading the Input

```python
n, clicks = map(int, input().split())
```

Suppose the input is:

```text
1000 45
```

`input()` reads:

```text
"1000 45"
```

`.split()` separates it:

```text
["1000", "45"]
```

`map(int, ...)` converts them into integers:

```text
1000
45
```

So:

```python
n = 1000
clicks = 45
```

---

# 15. Calling the Function

```python
p_hat, lower, upper = click_rate_band(n, clicks)
```

The function calculates the three values and returns them.

They are assigned to:

```text
p_hat
lower
upper
```

---

# 16. Formatting the Output

```python
print(f"{p_hat:.6f} {lower:.6f} {upper:.6f}")
```

The problem requires exactly **6 digits after the decimal point**.

The format:

```python
:.6f
```

means:

> Display this number as a floating-point number with 6 digits after the decimal point.

For example:

```text
0.045
```

becomes:

```text
0.045000
```

---

# 17. Complexity Analysis

There are only a constant number of arithmetic operations.

Therefore:

### Time Complexity

$$
\boxed{O(1)}
$$

The input can contain values up to:

$$
10^9
$$

but the algorithm does not loop through `n` elements.

### Space Complexity

Only a few variables are stored.

$$
\boxed{O(1)}
$$

---

# 18. Important Edge Cases

The constraints guarantee:

$$
1\leq clicks\leq n\leq10^9
$$

So `clicks` is never zero.

However, `clicks` can equal `n`.

For example:

```text
n = 100
clicks = 100
```

Then:

$$
\hat p=1
$$

and:

$$
SE=
\sqrt{\frac{1(1-1)}{100}}
=0
$$

Therefore:

$$
lower=upper=1
$$

The interval collapses to a single point.

This follows directly from the given formula; no special-case code is required.

---

# 19. Why This Problem Is Useful

Although the implementation is short, the problem combines several important ideas:

```text
Probability
     ↓
Bernoulli trials
     ↓
Sample proportion
     ↓
Sampling variability
     ↓
Standard error
     ↓
Normal approximation
     ↓
Confidence interval
     ↓
Implementation
```

The most important lesson is that **a point estimate is not the same thing as certainty**.

A CTR of 4.5% is an estimate based on observed data. The confidence interval gives us information about the uncertainty associated with that estimate.

---

# 20. Final Formula Cheat Sheet

For a total of `n` observations and `clicks` successes:

### Point estimate

$$
\boxed{
\hat p=\frac{clicks}{n}
}
$$

### Standard error

$$
\boxed{
SE=
\sqrt{\frac{\hat p(1-\hat p)}{n}}
}
$$

### 95% confidence interval

$$
\boxed{
\hat p\pm1.959964\times SE
}
$$

### Lower bound

$$
\boxed{
lower=\hat p-1.959964SE
}
$$

### Upper bound

$$
\boxed{
upper=\hat p+1.959964SE
}
$$

### Complexity

$$
\boxed{Time=O(1)}
$$

$$
\boxed{Space=O(1)}
$$
