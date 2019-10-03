# CSCC37

## Tutorial

### TUT 1: Tuesday, September 24, 2019

**Saba.Kiaei@mail.utoronto.ca**

- Conversion
  - From base $b$ to base 10
    - $\pm (d_n d_{n-1}...d_0 . d_{-1}d_{-2}...)_b = \pm (d_n b^n + ... + d_0 b^0 + d_{-1} b^{-1} + ...)_{10}$
  - From 10 to base $b$

**Example:** Converting $(72.6)_{10}$ to base 3.

| Numerator | Denominator | Quotient | Remainder |
| --------- | ----------- | -------- | --------- |
| 72        | 3           | 24       | 0         |
| 24        | 3           | 8        | 0         |
| 8         | 3           | 2        | 2         |
| 2         | 3           | 0        | 2         |

So we read up the Remainder and we get $(72)_{10} = (2200)_3$

Now we will do the decimal.

| Multiplier | Base | Product | Integral | Fraction |
| ---------- | ---- | ------- | -------- | -------- |
| 0.6        | 3    | 1.8     | 1        | 0.8      |
| 0.8        | 3    | 2.4     | 2        | 0.4      |
| 0.4        | 3    | 1.2     | 1        | 0.2      |
| 0.2        | 3    | 0.6     | 0        | 0.6      |
| 0.6        | 3    | 1.8     | 1        | 0.8      |

We see a pattern, so it's repeating $(0.\bar{0121})_3 = (0.6)_{10}$

So we have $(72.6)_{10} = (2200.\bar{1210})_3 = 2.200\bar{1210} \times 10^3$

But our mantissa length is 8, so we need to round

$2.200\bar{1210} \times 3^3 \longrightarrow fl(x) = 2.2001210 \times 3^3 $

**Example**: Floating Point Number $\mathbb{R}_3 (t = 8, e \in [-2,4])$

Find the Absolute Rounding Error

$\delta = \frac{x - fl(x)}{x}$ (This is the Relative Error)

$x-fl(x)$ (This is the Rounding Error)

The absolute error for our previous example is: $x - fl(x) = 0.0000000\bar{1210}$

#### Addition with Floating Point Numbers

To add $x+y$ we do $fl(fl(x) + fl(y))$ which then we can turn into

$(x+y)(1-\delta)$ where $\delta \leq \frac{|x|+|y|}{|x+y|}2eps \begin{cases} 2eps & xy > 0\\ x \approx -y \\ |\frac{x-y}{x+y}| & xy < 0 \end{cases}$

However, we have problems calculating $1-\cos (x)$ if $x$ is close to $0$.

But if we multiply this by $\frac{1 + \cos (x)}{1 + \cos (x)} = 1$ then...

$(1-\cos x)\frac{1 + \cos (x)}{1 + \cos (x)} = \frac{1+\cos x - (\cos x + \cos^2 x)}{1+cos(x)} = \frac{\sin^2 x}{1 + \cos x}$

You compute the answer differently based on which x is approaching.

We use $(1-\cos x)$ if $x$ is not close to 0

We use $\frac{\sin^2 x}{1 + \cos x}$ if $x$ is not close to $\frac{\pi}{2}$

**Example:** $A = ln(8) - ln(15) - ln(33) + ln(62)$, evalue this in a $4$ digit base 10 system.

$ln(8) = 2.079$

$ln(15) = 2.708$

$ln(33) = 3.497$

$ln(62) = 4.127$

Calculating each one by itself is $1.000 \times e^{-3}$, but the answer is $A = 2.108 \times e^{-3}$

So the absolute error is $1.108 \times e^{-3}$, and the relative error is around 0.5

This is because for each $ln$ operation we do, we convert it into a float and it becomes inaccurate, so we need to remove the amount of $ln$s in the problem.

We can use the taylor expansion!

$ln(1+u) = u - \frac{u^2}{2} + \frac{u^3}{3} - ...$

So we can convert $A = ln(\frac{8 \times 62}{15 \times 32}) = ln(1 + \frac{1}{495}) \approx 1 + \frac{1}{495}$

And the taylor expansion is safer to compute.