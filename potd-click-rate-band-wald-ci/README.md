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

<div align="center">
0.5 = 50%
</div>

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

* \($\hat p\$) = observed proportion
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
## 📐 Detailed Mathematical Derivation

The goal is to derive the formula used to calculate the 95% confidence interval for the click-through rate:

$$
\hat{p} \pm z \cdot SE
$$

where:

$$
\hat{p} = \frac{clicks}{n}
$$

and

$$
SE = \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}
$$

---

### 1. Model Each User's Click

For every user, define a random variable $X_i$:

$$
X_i =
\begin{cases}
1, & \text{if the user clicks} \\
0, & \text{if the user does not click}
\end{cases}
$$

Let $p$ be the true probability that a user clicks the advertisement.

Therefore:

$$
P(X_i=1)=p
$$

and

$$
P(X_i=0)=1-p
$$

This is called a **Bernoulli random variable**.

---

### 2. Expected Value of One User's Click

The expected value of a random variable is:

$$
E[X_i] = \sum_x xP(X_i=x)
$$

For our Bernoulli variable, $X_i$ can only be $0$ or $1$:

$$
E[X_i]
=
(1)(p)+(0)(1-p)
$$

Therefore:

$$
\boxed{E[X_i]=p}
$$

So, the average value of the click variable is equal to the true click probability.

---

### 3. Variance of One User's Click

Variance measures how much a random variable varies around its expected value.

The variance formula is:

$$
Var(X_i)=E[X_i^2]-(E[X_i])^2
$$

Since $X_i$ can only be $0$ or $1$:

$$
X_i^2=X_i
$$

because:

$$
0^2=0
$$

and

$$
1^2=1
$$

Therefore:

$$
E[X_i^2]=E[X_i]=p
$$

We already know:

$$
E[X_i]=p
$$

Hence:

$$
Var(X_i)=p-p^2
$$

Factoring:

$$
\boxed{Var(X_i)=p(1-p)}
$$

---

### 4. Calculate the Observed Click Rate

Suppose we observe $n$ users.

The total number of clicks is:

$$
X_1+X_2+\cdots+X_n
$$

Therefore, the observed click rate is:

$$
\hat{p}
=
\frac{X_1+X_2+\cdots+X_n}{n}
$$

or equivalently:

$$
\boxed{
\hat{p}=\frac{clicks}{n}
}
$$

Here, $\hat{p}$ is called the **sample proportion** or **point estimate** of the true probability $p$.

---

### 5. Variance of the Sample Proportion

We now want to determine how much $\hat{p}$ varies from one sample to another.

We have:

$$
\hat{p}
=
\frac{X_1+X_2+\cdots+X_n}{n}
$$

Therefore:

$$
Var(\hat{p})
=
Var\left(
\frac{X_1+X_2+\cdots+X_n}{n}
\right)
$$

Using the property:

$$
Var(cX)=c^2Var(X)
$$

we get:

$$
Var(\hat{p})
=
\frac{1}{n^2}
Var(X_1+X_2+\cdots+X_n)
$$

Assuming that the users' click outcomes are independent:

$$
Var(X_1+X_2+\cdots+X_n)
=
Var(X_1)+Var(X_2)+\cdots+Var(X_n)
$$

Each user has:

$$
Var(X_i)=p(1-p)
$$

Since there are $n$ users:

$$
Var(X_1+\cdots+X_n)
=
np(1-p)
$$

Therefore:

$$
Var(\hat{p})
=
\frac{1}{n^2}
\left[np(1-p)\right]
$$

Cancel one factor of $n$:

$$
\boxed{
Var(\hat{p})
=
\frac{p(1-p)}{n}
}
$$

---

### 6. Deriving the Standard Error

The standard deviation of an estimator is called its **standard error**.

Therefore:

$$
SE(\hat{p})
=
\sqrt{Var(\hat{p})}
$$

Substituting the variance we derived:

$$
SE(\hat{p})
=
\sqrt{
\frac{p(1-p)}{n}
}
$$

Thus:

$$
\boxed{
SE(\hat{p})
=
\sqrt{\frac{p(1-p)}{n}}
}
$$

However, there is a problem.

We do not know the true value of $p$.

The entire purpose of collecting data is to estimate $p$.

Therefore, we replace the unknown $p$ with our observed estimate $\hat{p}$.

Hence:

$$
\boxed{
SE
=
\sqrt{
\frac{\hat{p}(1-\hat{p})}{n}
}
}
$$

This is the formula used in the problem.

---

## 7. Why Do We Use a Normal Distribution?

For sufficiently large sample sizes, the **Central Limit Theorem (CLT)** tells us that the sampling distribution of the sample proportion $\hat{p}$ is approximately normal.

Therefore:

$$
\hat{p}
\approx
N
\left(
p,
\frac{p(1-p)}{n}
\right)
$$

After standardizing:

$$
Z
=
\frac{\hat{p}-p}{SE}
$$

approximately follows the standard normal distribution:

$$
Z\sim N(0,1)
$$

---

## 8. The 95% Confidence Level

For a standard normal distribution, approximately 95% of the probability lies between:

$$
-1.959964
$$

and

$$
+1.959964
$$

Therefore:

$$
P(-1.959964\leq Z\leq1.959964)
\approx0.95
$$

Substitute:

$$
Z=\frac{\hat{p}-p}{SE}
$$

giving:

$$
P
\left(
-1.959964
\leq
\frac{\hat{p}-p}{SE}
\leq
1.959964
\right)
\approx0.95
$$

---

## 9. Rearranging the Inequality

Starting with:

$$
-1.959964
\leq
\frac{\hat{p}-p}{SE}
\leq
1.959964
$$

Multiply all parts by $SE$:

$$
-1.959964SE
\leq
\hat{p}-p
\leq
1.959964SE
$$

Rearranging to isolate $p$:

$$
\hat{p}-1.959964SE
\leq
p
\leq
\hat{p}+1.959964SE
$$

Therefore, the 95% confidence interval is:

$$
\boxed{
\hat{p}
\pm
1.959964SE
}
$$

The lower bound is:

$$
\boxed{
Lower=
\hat{p}-1.959964SE
}
$$

The upper bound is:

$$
\boxed{
Upper=
\hat{p}+1.959964SE
}
$$

---

# 🔢 Complete Example

Suppose:

$$
n=1000
$$

and:

$$
clicks=45
$$

### Step 1: Calculate the Point Estimate

$$
\hat{p}
=
\frac{clicks}{n}
$$

$$
\hat{p}
=
\frac{45}{1000}
$$

$$
\boxed{\hat{p}=0.045}
$$

As a percentage:

$$
0.045\times100=4.5\%
$$

---

### Step 2: Calculate the Standard Error

The formula is:

$$
SE
=
\sqrt{
\frac{\hat{p}(1-\hat{p})}{n}
}
$$

Substitute the values:

$$
SE
=
\sqrt{
\frac{0.045(1-0.045)}{1000}
}
$$

$$
=
\sqrt{
\frac{0.045(0.955)}{1000}
}
$$

$$
\approx0.006556
$$

Therefore:

$$
\boxed{SE\approx0.006556}
$$

---

### Step 3: Calculate the Margin of Error

The margin of error is:

$$
ME=z\times SE
$$

where:

$$
z=1.959964
$$

Therefore:

$$
ME
=
1.959964\times0.006556
$$

$$
\boxed{ME\approx0.012849}
$$

---

### Step 4: Calculate the Lower Bound

$$
Lower=\hat{p}-ME
$$

$$
Lower=0.045-0.012849
$$

$$
\boxed{Lower\approx0.032151}
$$

---

### Step 5: Calculate the Upper Bound

$$
Upper=\hat{p}+ME
$$

$$
Upper=0.045+0.012849
$$

$$
\boxed{Upper\approx0.057849}
$$

Therefore, the final result is:

$$
\boxed{
0.045000\quad0.032151\quad0.057849
}
$$

Or in percentage form:

$$
\boxed{
4.5\%\quad[3.2151\%,5.7849\%]
}
$$

---

# 🧠 Complete Derivation at a Glance

The entire derivation can be summarized as:

$$
X_i\in\{0,1\}
$$

$$
E[X_i]=p
$$

$$
Var(X_i)=p(1-p)
$$

$$
\hat{p}
=
\frac{1}{n}
\sum_{i=1}^{n}X_i
$$

$$
Var(\hat{p})
=
\frac{p(1-p)}{n}
$$

$$
SE(\hat{p})
=
\sqrt{\frac{p(1-p)}{n}}
$$

Since $p$ is unknown:

$$
\boxed{
SE
=
\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}
}
$$

Using the normal approximation:

$$
\boxed{
CI_{95\%}
=
\hat{p}
\pm
1.959964\times SE
}
$$

Therefore:

$$
\boxed{
CI_{95\%}
=
\hat{p}
\pm
1.959964
\sqrt{
\frac{\hat{p}(1-\hat{p})}{n}
}
}
$$

This is the complete formula implemented by the program.

---

## ⚠️ Technical Note

The interval derived above is called the **Wald confidence interval** for a binomial proportion.

It is simple and computationally efficient, which is why it is used in this problem.

However, the Wald interval can perform poorly when:

- $n$ is small
- $\hat{p}$ is very close to $0$
- $\hat{p}$ is very close to $1$

For real-world statistical analysis, alternatives such as the **Wilson interval** or **exact binomial confidence interval** are often preferred.

For this programming problem, however, we must use the specified Wald formula.
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
