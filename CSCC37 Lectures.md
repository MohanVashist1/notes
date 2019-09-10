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