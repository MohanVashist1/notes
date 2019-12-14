# LEC 21

## Linear Programming Continued

Example: Maximize $3x_1 + 2x_2$ subject to:

- $x_1 \leq 10$
- $2x_1 + x_2 \leq 40$
- $x_1 + 3x_2 \leq 100$
- $x_1, x_2 \geq 0$

In this example, the maximum is one of the points of the polygon.

<u>Fact:</u> If an optimal solution to a Linear Program exists, then at least one optimal solution is a vertex of the feasible region.

This restricts the search for the optimal solution.

We can represent the objective function as

$c = (c_1,...,c_n), x=(x_1,..., x_n)$

so $c_1 x_1 + ... + c_n x_n = c \cdot x$

And the max of this is

$\frac{c \cdot x}{|c|}$ (length of projects of $x$ on $c$)

Note that an Optimal Solution to LP might not exist because

- LP is infeasible: feasible region is empty
- LP is unbounded (underconstrained)

LP: maximize objective function subject to constraints

<u>Input:</u> LP

<u>Output:</u>

- infeasible
- unbounded
- values for $x_1,...,x_n$ that max/min the objective function and satisfy all the constraints.

<u>LP Terminology</u>

- objective function: function to be min/max
- solution: assignment of real values ot the vars
- feasible solution: solution that satisfies all constraints
- optimal solution: feasible solution that min/max objective function
- value (cost) of solution: value of objective function at some solution
- value (cost) of LP: value of objective function at optimal solution

## Linear Programming Algorithms

- Simplex Algorithm (Dantzig 1947) (Kantorovitch 1939)
  - This is the most commonly used
  - Very good in practice
  - Exponential Complexity in the Worst Case

Khatchian 1979 came up with the ellipsoid algorithm, which is LP

- polytime in worst case
- but slow in practice

Karmakar 1984 - interior point method

- polytime in worst case
- good in practice

We will be using these algorithms as black box LP solvers

Efficient reduction to LP (polynomial number of variables and constraints)

Known polytime LP algorithms are polynomial in # of variables, # of constraints, and in size of coefficients

## Max Flow (Application of LP)

for a graph $G = (V,E)$

1. variables: $x_e \forall e \in E$ [$x_e$ flow through e]
2. objective function: max $\sum_{e\in out(S)} x_e$
3. constraints: $\forall e \in E, x_e \geq 0, x_e \leq c(e)$, and $\forall v \in V - \{s,t\}, \sum_{e \in in(v)} x_e = \sum_{e\in out(v)}$

## Line Fitting (Application of LP)

Input:

- $m$ points $p_1,...,p_m$, where $p_i = (p_{i1},...,p_{id})$
- labels $l_1,..., l_m$

Output: 

- linear function $h: \mathbb{R}^d \mapsto \mathbb{R}$
- $h(x_1,...,x_d) = a_1x_1 + ... + a_d x_d + b = (a = (a_1,..., a_n),b)$ The $a,b$ is our unknown variables

We're looking for the variables $(a,b)$ such that $h(p_i) \approx l_i, 1 \le i \le m$ (we must also define what we mean by $\approx$)

$E_i(a,b) = |a_1p_{i1} + ... + a_d p_{id} + b -l_i|$

This is the error with respect to $p_i$

We want to minimize $E(a,b) = \sum_{1 \leq i \leq m} E_i (a,b)$

<u>The Linear Program</u> is minimizing $\sum_{1 \leq i \leq m} |b + \sum_{j =1}^d a_j p_{ij} - l_i|$

The variables being $a=(a_1,..., a_d), b$

The constraints are: nothing, no constraints.

What is the problem with this? There is something nonlinear here. Absolute value is not linear.

Note that $|x| = max(x,-x)$

So instead of minimizing $|x|$, we can minimize $y$ subject to the constraints that $y \geq x$, $y \geq -x$

So by this trick, we got rid of the absolute value.

<u>LP</u>

- variables: $a=(a_1,..., a_d), b; y_1,...y_m$
- objective function: minimize $y_1+...+y_m$
- constraints: $y \geq b + \sum_{j =1}^d a_j p_{ij} - l_i$, $y \geq -(b + \sum_{j =1}^d a_j p_{ij} - l_i)$





