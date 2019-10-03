# CSCC37

## Lecture Notes

### LEC 1: Monday, September 9, 2019

#### Course Outline

- Floating Point Arithmetic - Can these examples be represented on a computer?
  - $\pi$? no
  - $\sqrt{2}$? no
  - $\frac{1}{10} = (0.1)_{10}$? no
- Error Propogation / Rounding Error
  - <u>Example:</u> A 4 digit mantissa computer with rounding (mantissa is the number of digits that can be stored)
    - $0.1234367 - 0.1234216$ is stored as $0.1234 - 0.1234$ so the computer results in 0. The true answer is $0.151 \times 10^{-4}$
    - We can mitigate this by working with smaller magnitude digits first before moving on to larger ones.
- Conditioning / Stability
  - measure how small pertubations are in initial input
- Linear Systems of Equations
  - <u>problem</u>: solve where $A\underline{x} = \underline{b} | A \in \mathbb{R}^{n \times n}, \underline{b} \in \mathbb{R}^n$
  - $\underline{x} \in\mathbb{R}^n$ is unknown, and needs to be solved for
  - one possibility: Gaussian Elimination (Direct Method). The process is as follows
    - Factor $A$ into $A = LU$ where $L$ is the lower triangle and $U$ is the upper triangle (where the other part of the triangle is 0 for both of them).
    - Now $A\underline{x} = \underline{b}$ iff $LU\underline{x} = \underline{b} | U\underline{x} = \underline{d} $
      - Now we solve $L\underline{d} = \underline{b}$ For $\underline{d}$ (forward elimination)
      - Now we solve $U\underline{x} = \underline{d}$ For $\underline{x}$ (backward substitution)
      - Note: we should not be inverting matrices as it is really expensive and is not stable.
  - another posibility: Iterative Methods (alternative to Direct Method)
    - Note that Gaussian Elimination is $O(n^3), A \in \mathbb{R}^{n \times n}$
    - $A\underline{x} = \underline{b}$ iff $(L + D + U)\underline{x} = \underline{b}$ where $L$ is the lower triangle of $A$, $D$ is the diagonal of $A$ and $U$ is the upper triangle of $A$.
    - $A\underline{x} = \underline{b}$
    - $(L + D + U)\underline{x} = \underline{b}$
    - $D\underline{x} = - (L+U)\underline{x} + \underline{b} = \underline{c}$ which results in $x_1 = \frac{c_1}{d_1}$,$x_2 = \frac{c_2}{d_2}$,..., $x_n = \frac{c_n}{d_n}$
    - This complexity is $O(n)$ as it is $n$ divisions
    - But $\underline{c} = - (L+U)\underline{x} + \underline{b}$ is not something we can do as $\underline{x}$ is still unknown.
      - We can solve $D\underline{x} = - (L+U)\underline{x} + \underline{b} = \underline{c}$ by iteration
      - $D\underline{x}^{k+1} = - (L+U)\underline{x}^{k} + \underline{b} = \underline{c}$ We start with an initial guess at the solution, let's say that $\underline{x}^0=[0,...., 0]^T$ then iterate until convergence.
      - How do we measure? 
        - $||x^{k+1} - x^k||_2 < $ tolerance factor (X-Test) (might converge to something that isn't the solution)
        - $||\underline{b} - A\underline{x}^{k+1}||_2 < $ tolerance factor (F-Test)
        - Which test is more reliable? Possible Assignment 1 question.
  - Iterative Refinement
- Non-Linear Equations (single equation)
  - <u>problem:</u> solve $F(x) = 0$ for $x^*$ where $F: \mathbb{R} \mapsto \mathbb{R}, x \in\mathbb{R}$
  - $x^*$ is a root of $F(x) \mapsto F(x^*) = \emptyset$
    - Is there a solution?
    - How many solutions?
  - Algorithms based on the fixed point problem
    - <u>Idea</u> $F(x) = 0 \leftrightarrow x = g(x)$ where the first point on the left hand side is root $x^*$ and the right hand sign is fixedpoint $x^*$.
    - Can always use $g(x) = x - F(x)$ or $g(x) = x - h(x)F(x)$ where $h(x)$ is an auxiliary function
  - Fixed Point Iteration
    - How to solve the Fixed point Problem
    - Initial guess: $x^0 = ?$ (often 0)
    - then iterate $x^{k+1} = g(x^k)$
  - Newton's Method for $F(x)=0$
    - $x^{k+1} - x^k - \frac{F(x^k)}{F'(x^k)}$
    - second form with $h(x) = \frac{1}{F'(x)}$

### LEC 2: Monday, September 16, 2019

- Approximation / Interpolation
  -  data fitting
  - <u>example:</u> find a line that goes through $\{ (t_0, y_0), (t_1, y_1) \}$ equation of a line $a_0 + a_1 t = y$. Find $a_0$ and $a_1$ such that $a_0 + a_1t_0 = y_0$ and $a_0 + a_1 t_1 = y_1$ or we can relabel this as $Ax=b, A \in \mathbb{R}^{2\times 2}, x,b \in \mathbb{R}^2$.
  - <u>example:</u> find a line that goes through $\{ (t_0, y_0), (t_1, y_1), (t_2, y_2) \}$ equation of a line $a_0 + a_1 t = y$. Find $a_0$ and $a_1$ such that $a_0 + a_1t_0 = y_0$ and $a_0 + a_1 t_1 = y_1$ and $a_0 + a_1 t_2 = y_2$,  or we can relabel this as $Ax=b, A \in \mathbb{R}^{2\times 3}, x,b \in \mathbb{R}^2$. Note that $A$ is not a squre matrix.
- Numerical Integration / Quadrative
  - <u>problem</u>: estimate $\int^b_a F(x)dx$
  - <u>basic idea</u>: integrate a piecewise interpolant exactly (break up a curve into multiple small staight lines.)
  - Then $\int^b_a F(x)dx \thickapprox \sum_i T_i$ where $T_i, i = 0,...,n$ are $n$ trapezoids that the function breaks into.
  - **Interpolants** are the piecewise sections used for approximating a function

#### What is Numerical Analysis?

- Physical Systems
  - ex. Space Stuff, Weather Stuff, Climate Stuff
- Mathematical Model
  - Linear and Non Linear Equations
  - Differential Equations
- Analytical Solution
  - Solution that works out in terms of the math, but is not a numerical solution
- Numerical Solution
  - The actual solution as a number

#### Why Mathematical Models?

- Often cheaper than physical models
- more flexible
- often the only approach

#### Why Numerical Solutions?

- often the only approach: analytical solution does not exist
- often cheaper than analytical solutions

#### Converting base $b$ to decimal

**example:** recall that $b$ has to be a natural number. let us convert from $b=16$ (hexadecimal)

base 16 symbols: 0 1 2 3 4 5 6 7 8 9 A B C D E F

$\begin{align*} (8FA)_{16} &= 8\times 16^2 + F\times 16^1 + A\times 16^0 \\ &= 8(16^2) + 15(16) + 10(16^0) \\ &= (2198)_{10} \end{align*}$

#### Converting Decimal to base b

**example:** $b=2$ What is $(350)_{10}$ in base 2?

| Numerator | Denominator | Quotient | Remainder |
| --------- | ----------- | -------- | --------- |
| 350       | 2           | 175      | 0         |
| 175       | 2           | 87       | 1         |
| 87        | 2           | 43       | 1         |
| 43        | 2           | 21       | 1         |
| 21        | 2           | 10       | 1         |
| 10        | 2           | 5        | 0         |
| 5         | 2           | 2        | 1         |
| 2         | 2           | 1        | 0         |
| 1         | 2           | 0        | 1         |

We stop when the quotient is 0.

We then read the remainder digits from the bottom to the top and we have our conversion: $(101011110)_2$

This conversion is <u>safe</u> (other than overflow)

#### Representation of Reals

if $x\in\mathbb{R}$, then $\begin{align*}x &= \pm (x_i \cdot x_F)_b\\ &= \pm (d_n d_{n-1}... d_0 . d_{-1} d_{-2} ....)_b \end{align*}$

$x_I$ is called the integral part

$x_F$ is called the fraction

The sign ($+$ or $-$) is one bit 0 or 1

$x_I$ is a non-negative integer

$x_F$ can have an infinite number of digits

**example:** $(0.\bar7)_{10} = 7 \times 10^{-1} + 7 \times 10^{-2} + ...$

### LEC 3: Monday, September 23, 2019

#### Representation of the Reals

If $x \in \mathbb{R}$ then $x = \pm (x_I \cdot x_F)_b = \pm (d_n d_{n-1}...d_0 \cdot d_{-1} d_{-1} ...)$

For binary ststem ($b=2$)

$\begin{align*} (.000110011....)_2 &= (.0\bar{0011})_2 \\ &= 0\cdot2^{-1} + 0\cdot 2^{-2} + 0\cdot 2^{-3} +1\cdot 2^{-4} + ... \end{align*}$

For base $b$ system

$x_F = (.d_{-1}d_{-2}d_{-3}...)_b = d_{-1} b^{-1} + d_{-2} b^{-2} + .... = \sum^\infty_{i=1} d_{-i} b^{-i}$

Note: A terminating <u>binary</u> Fraction with $n$ digits has a terminating decimal fraction representation.

Converting base $b$ fractions to decimal? See above.

Converting decimal fractions to base $b$ ($b=2$)

<u>example:</u> What is $(.625)_{10}$ in binary?

| multiplier | base | product | integral | fraction |
| ---------- | ---- | ------- | -------- | -------- |
| .625       | 2    | 1.25    | 1        | .25      |
| .25        | 2    | 0.5     | 0        | .5       |
| .5         | 2    | 1       | 1        | 0        |

Then you read the integral part from up to down.

$(.625)_{10} = (.101)_2$

<u>example:</u> What is $(.1)_{10}$ in binary?

| multiplier | base | product | integral | fraction |
| ---------- | ---- | ------- | -------- | -------- |
| .1         | 2    | 0.2     | 0        | .2       |
| .2         | 2    | 0.4     | 0        | .4       |
| .4         | 2    | 0.8     | 1        |          |
| .8         | 2    | 1.6     | 1        |          |
| .6         | 2    | 1.2     | 0        |          |
| .2         | 2    | 0.4     | 0        |          |

This pattern keeps going and going, it doesn't terminate. $(.1)_{10} = (.0\bar{0011})_2$. It's a terminating decimal fraction that turns into a binary non terminating fraction. This can be expressed as an infinite sum with a finite result.

#### Machine Representation of Reals

Reals represented in computer as floating point numbers. A floating point number $x$ in base $b$ has the form:

$x = (F)_b \cdot b^{(e)_b}$ where $e$ is an exponent.

Fraction $F = \pm (. d_1 d_2...d_t)$ is called the **mantissa** and $e = \pm (e_s e_{s-1} ... e_1)_b$ is called the ($s$ digit) **exponent**

The Floating point number is **noramlized** if $d_1 \neq 0$ unless $d_1 = d_2 = ... = d_t = 0$

**Significant digits** (of a non-zero floating point number) are the digits following and include the first non zero digit. All digits of the manitssa of a normalized Floating Point numbers are significant.

Absolute value of mantissa is always $\geq 0$ and $< 1$.

Exponent is limited: $-M \leq e \leq M$ where $M = (aa...a)_b$ is a $s$ digit number and $a = b-1$. 

The largest floating point number in absolute value is $t$ digit $(.aa....a)_b$ multiplied by $b^{(aa...a)_{b}}$ where the exponent has $s$ digits and $(a=b-1)$

The smallest floating point number in absolute value, non zero is $(.1000....0)_b \cdot b^{-(aa...a)_b}$ where $(a=b-1)$ and the exponent has $s$ digits and the base has $t$ digits.

The non-normalized version (the first digit can be 0) will result in the real smallest number possible.

$\mathbb{R}_b(t,s)$ is the set of all base $b$ floating point numbers with absolute value inside these ranges

**Overflow** or **underflow** occur whenever an non-zero floating point number with absolute value outside of their ranges must be stored on the computer.

- Underflowing is being too close to 0, overflow is being an absolute value that is too large.

Note that $\mathbb{R}_b(t,s)$ is <u>finite</u>, whereas $\mathbb{R}$ is <u>infinite</u>.

Also, $\mathbb{R}$ is compact whereas $\mathbb{R}_b(t,s)$ is not.

fgk

#### Machine Arithmetic

Let $x,y \in \mathbb{R}$ and $Fl(x), Fl(y) \in \mathbb{R}_b (t,s)$

Consider $\circ \in \{ +, -, \cdot, /\}$

Does a computer give $x \circ y$ ? No.

$Fl(x) \circ Fl(y)$? No.

Computer gives $Fl(Fl(x) \circ Fl(y))$. ie.e $x\circ y \approx Fl(Fl(x) \circ Fl(y))$

<u>Example:</u> in $\mathbb{R}_{10} (2,4), x = 2, y = 0.000058$

(In $\mathbb{R}, x+y = 2 + 0.000058 = 2.000058$)

$Fl(x) = (+0.20 \cdot 10^1)_{10}$

$Fl(x) = (+0.58 \cdot 10^{-5})_{10}$

Note: no RRO in $Fl(x) = x, Fl(y) = y$

So $0.20 \cdot 10^1 + 0.58 \cdot 10^{-5} = 0.20000058 \cdot 10^1$

This result is only stored temporarily. We will need to store in 2-digit mantissa.

Then $Fl(Fl(x) \circ Fl(y)) = +0.20 \cdot 10^1$ (the 0.00000058 was truncated).

#### Machine Precision (or machine epsilon or eps)

The smallest non-normalized Floating Point Number eps such that $1 + eps > 1$ is called machine precision or machine epsilon.

$eps = \begin{cases}b^{1-t} & \text{chopping} \\ \frac{1}{2}b^{1-t} & \text{rounding}\end{cases}$

Recall $\delta = \frac{x - Fl(x)}{x}$ is the RRO.

$\begin{cases} 0 \leq \delta \leq eps & \text{chopping} \\ -eps \leq \delta \leq eps & \text{rounding} \end{cases}$

### LEC: Monday, September 30, 2019

How exactly is error propogated in each of $\circ \in \{ +, -, \cdot, / \}$?

Let $x,y \in \mathbb{R}$. Then $Fl(x) = x(1-\delta x), Fl(y) = y(1-\delta y)$

<u>Multiplication:</u> $x \cdot y$

Computer gives $\begin{align*} Fl(Fl(x) \cdot Fl(y)) &= [x(1-\delta_1), y (1-\delta_2)](1 - \delta_3) \\ &= x \cdot y (1 - \delta_1) (1-\delta_2) (1 - \delta_3) \\ &= x \cdot y (1 - \delta_1 - \delta_2 + \delta_1 \delta_2 + \delta_1 \delta_3 + \delta_2 \delta_3 - \delta_1 \delta_2 \delta_3) \\ &\approx x \cdot y (1 - \delta_1 - \delta_2 - \delta_3). \\ &= x \cdot y (1 - \delta_\cdot)\end{align*}$

