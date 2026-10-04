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

The goal is to derive the formula used to calculate the 95% confidence interval for the click-through rate.

The final formula is:

    Confidence Interval = p_hat ± z × SE

where:

    p_hat = clicks / n

and:

    SE = sqrt( p_hat × (1 - p_hat) / n )

For a 95% confidence interval:

    z = 1.959964

---

## 1. Model Each User's Click

For every user, define a variable X_i.

    X_i = 1  →  if the user clicks
    X_i = 0  →  if the user does not click

Let p be the true probability that a user clicks the advertisement.

Therefore:

    P(X_i = 1) = p

and:

    P(X_i = 0) = 1 - p

This type of random variable is called a Bernoulli random variable.

---

## 2. Expected Value of One User's Click

The expected value represents the average value we would obtain if we repeated the experiment many times.

For a Bernoulli random variable:

    E[X_i] = (1 × p) + (0 × (1 - p))

Therefore:

    E[X_i] = p

So:

    E[X_i] = p

This means that the expected value of a user's click indicator is equal to the true click probability.

For example, if the true click probability is 0.05, then over a very large number of users, the average value of X_i will approach 0.05.

---

## 3. Variance of One User's Click

Variance measures how much a random variable varies around its expected value.

The variance formula is:

    Var(X_i) = E[X_i²] - (E[X_i])²

Since X_i can only be 0 or 1:

    0² = 0
    1² = 1

Therefore:

    X_i² = X_i

So:

    E[X_i²] = E[X_i]

And we already know:

    E[X_i] = p

Therefore:

    E[X_i²] = p

Substituting into the variance formula:

    Var(X_i) = p - p²

Factor out p:

    Var(X_i) = p(1 - p)

Therefore:

    Var(X_i) = p(1 - p)

This is the variance of one Bernoulli trial.

---

## 4. Calculate the Observed Click Rate

Suppose we observe n users.

The total number of clicks is:

    X_1 + X_2 + X_3 + ... + X_n

Therefore, the observed click rate is:

    p_hat = (X_1 + X_2 + ... + X_n) / n

Since the sum represents the total number of clicks:

    p_hat = clicks / n

Here:

    p_hat = observed click rate
    clicks = number of successful clicks
    n = total number of users

p_hat is called the sample proportion or point estimate.

It is our estimate of the unknown true probability p.

---

## 5. Derive the Variance of the Sample Proportion

We now want to know:

    How much can p_hat vary from one sample to another?

We have:

    p_hat = (X_1 + X_2 + ... + X_n) / n

Therefore:

    Var(p_hat)
    = Var((X_1 + X_2 + ... + X_n) / n)

Using the property:

    Var(cX) = c² × Var(X)

we get:

    Var(p_hat)
    = (1 / n²) × Var(X_1 + X_2 + ... + X_n)

---

## 6. Add the Variances

Assume that the users' click outcomes are independent.

For independent random variables:

    Var(X_1 + X_2 + ... + X_n)
    = Var(X_1) + Var(X_2) + ... + Var(X_n)

We already derived that:

    Var(X_i) = p(1 - p)

Every user has the same variance.

Since there are n users:

    Var(X_1 + X_2 + ... + X_n)
    = n × p(1 - p)

Therefore:

    Var(p_hat)
    = (1 / n²) × [n × p(1 - p)]

Cancel one n:

    Var(p_hat)
    = p(1 - p) / n

Therefore:

    Var(p_hat) = p(1 - p) / n

This is the variance of the sample proportion.

---

## 7. Derive the Standard Error

The standard error is the standard deviation of an estimator.

Therefore:

    SE(p_hat) = sqrt(Var(p_hat))

We already know:

    Var(p_hat) = p(1 - p) / n

Therefore:

    SE(p_hat)
    = sqrt(p(1 - p) / n)

So:

    SE(p_hat) = sqrt(p(1 - p) / n)

---

## 8. Replace p with p_hat

There is a problem with the formula above.

We do not know the true value of p.

Remember:

    p = true click probability

The entire purpose of our experiment is to estimate p.

However, we do know the observed value:

    p_hat = clicks / n

Therefore, we estimate the standard error by replacing p with p_hat.

So:

    SE = sqrt(p_hat × (1 - p_hat) / n)

This is the formula used in the problem.

Therefore:

    SE = sqrt( p_hat × (1 - p_hat) / n )

---

## 9. Why Can We Use the Normal Distribution?

For a sufficiently large sample size, the Central Limit Theorem tells us that the sampling distribution of p_hat is approximately normal.

In other words, if we repeatedly collect samples of size n and calculate p_hat for each sample, the values of p_hat will approximately form a normal distribution.

The center of this distribution is:

    p

and its standard deviation is approximately:

    SE = sqrt(p(1 - p) / n)

Therefore, p_hat is approximately normally distributed around the true value p.

---

## 10. Standardizing the Distribution

For a normal distribution, we can convert our value into a standard normal variable.

The standardized value is:

    Z = (p_hat - p) / SE

For a standard normal distribution:

    Z ~ N(0, 1)

For a 95% confidence interval, approximately 95% of the standard normal distribution lies between:

    -1.959964 and +1.959964

Therefore:

    -1.959964 <= Z <= 1.959964

Substituting:

    Z = (p_hat - p) / SE

we get:

    -1.959964
    <=
    (p_hat - p) / SE
    <=
    1.959964

---

## 11. Rearrange the Inequality

Start with:

    -1.959964 <= (p_hat - p) / SE <= 1.959964

Multiply everything by SE:

    -1.959964 × SE
    <=
    p_hat - p
    <=
    1.959964 × SE

We want p in the middle.

After rearranging:

    p_hat - 1.959964 × SE
    <=
    p
    <=
    p_hat + 1.959964 × SE

Therefore, the 95% confidence interval is:

    p_hat ± 1.959964 × SE

So:

    Lower = p_hat - 1.959964 × SE

    Upper = p_hat + 1.959964 × SE

---

# 🔢 Complete Numerical Example

Suppose:

    n = 1000

and:

    clicks = 45

---

## Step 1: Calculate p_hat

The sample click rate is:

    p_hat = clicks / n

Substitute the values:

    p_hat = 45 / 1000

Therefore:

    p_hat = 0.045

As a percentage:

    0.045 × 100 = 4.5%

So the observed click-through rate is:

    4.5%

---

## Step 2: Calculate the Standard Error

The formula is:

    SE = sqrt( p_hat × (1 - p_hat) / n )

Substitute:

    SE = sqrt( 0.045 × (1 - 0.045) / 1000 )

Calculate:

    1 - 0.045 = 0.955

Therefore:

    SE = sqrt( 0.045 × 0.955 / 1000 )

    SE ≈ 0.006556

So:

    SE ≈ 0.006556

---

## Step 3: Calculate the Margin of Error

The margin of error is:

    Margin of Error = z × SE

For a 95% confidence interval:

    z = 1.959964

Therefore:

    Margin of Error
    = 1.959964 × 0.006556

    Margin of Error ≈ 0.012849

---

## Step 4: Calculate the Lower Bound

The lower bound is:

    Lower = p_hat - Margin of Error

Substitute:

    Lower = 0.045 - 0.012849

Therefore:

    Lower ≈ 0.032151

---

## Step 5: Calculate the Upper Bound

The upper bound is:

    Upper = p_hat + Margin of Error

Substitute:

    Upper = 0.045 + 0.012849

Therefore:

    Upper ≈ 0.057849

---

# ✅ Final Result

The three values are:

    p_hat = 0.045000
    Lower = 0.032151
    Upper = 0.057849

Therefore, the program outputs:

    0.045000 0.032151 0.057849

In percentage form:

    4.5% [3.2151%, 5.7849%]

This means:

    Observed click rate = 4.5%

    Lower confidence bound ≈ 3.2151%

    Upper confidence bound ≈ 5.7849%

---

# 🧠 Complete Derivation at a Glance

The entire derivation can be summarized as follows:

    X_i = 1 if the user clicks
    X_i = 0 if the user does not click

For one user:

    E[X_i] = p

    Var(X_i) = p(1 - p)

For n users:

    p_hat = (X_1 + X_2 + ... + X_n) / n

Therefore:

    Var(p_hat) = p(1 - p) / n

Taking the square root:

    SE(p_hat) = sqrt(p(1 - p) / n)

Since p is unknown, replace it with p_hat:

    SE = sqrt(p_hat × (1 - p_hat) / n)

For a 95% confidence interval:

    z = 1.959964

Therefore:

    Confidence Interval
    = p_hat ± 1.959964 × SE

Substituting SE:

    Confidence Interval
    = p_hat ± 1.959964 ×
      sqrt(p_hat × (1 - p_hat) / n)

Therefore:

    Lower
    = p_hat - 1.959964 ×
      sqrt(p_hat × (1 - p_hat) / n)

    Upper
    = p_hat + 1.959964 ×
      sqrt(p_hat × (1 - p_hat) / n)

---

## ⚠️ Technical Note

The confidence interval used here is called the **Wald confidence interval** for a binomial proportion.

It is simple and computationally efficient, which is why it is used in this programming problem.

However, the Wald interval can perform poorly when:

- n is small
- p_hat is very close to 0
- p_hat is very close to 1

For real-world statistical analysis, methods such as the **Wilson interval** or **exact binomial confidence interval** are often preferred.

For this programming problem, however, the required formula is specifically the Wald interval, so we use it exactly as specified.
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
