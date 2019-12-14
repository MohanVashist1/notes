### LEC 20: Monday, November 18, 2019

#### Linear Programming (DPV 7.1, 7.4, 7.6, KT 11.6)

Optimization problems:

- optimize (min/max) object function subject to constraint

##### Diet Problem

- $n$ types of food $F_1, F_2, ..., F_n$
- $m$ types of nutrients $N_1, N_2,... N_m$
- Unit of $F_j, 1 \leq j \leq n$
  - costs $c_j$
  - provides $a_{ij}$ units of $N_i$

We must obtain $\geq b_i$ units of $N_i$

1. Variables: $X_1 ,..., x_n$ = amount of $F_j$ in diet $1 \leq j \leq n$

2. min $c_1 x_1 + ... + c_n x_n$

3. constraints:

   $a_{11}x_1 + a_{12}x_2 + ... + a_{1n} x_n \geq b_1$

   .

   .

   .

   $a_{m1}x_1 + a_{m2}x_2 + ... + a_{mn} x_n \geq b_m$

##### Transportation Problem

$k$ plants $P_1 ,..., P_k$

$l$ outlets $O_1 ,..,  O_l$

$P_i$ makes $s_i$ of some product

$O_j$ requires $d_j$ of that product

$c_{ij}$ is the cost of transporting unit of product $P_i$ to $O_j$

1. Variables $x_{ij} =$ amount shippsed from $P_i$ to $O_j$

2. Object Function: min $\sum_{1 \leq i \leq k, 1 \leq j \leq l} c_{ij} x_{ij}$

3. Constraints

   $\forall 1 \leq i \leq k, \sum_{1 \leq j \leq l} x_{ij} \leq s_i$

   $\forall 1 \leq j \leq l, \sum_{1 \leq j \leq l} x_{ij} \geq d_j$

   $x_{ij} \geq 0$

##### General Form of Linear Programs

1. Vars $x_1 ,..., x_n \in \mathbb{R}$

2. Object Function, min/max $\sum^n_{j=1} c_j x_j, c_j \in\mathbb{R}$

3. Constraints: $\sum^n_{j=1} a_{ij} x_j \dagger b_i$

   where $b_i, a_{ij} \in \mathbb{R}$ and $\dagger \in \{ \leq, =, \geq \}$

Input: $a_{ij}, b_i, c_j \in \mathbb{R} | 1 \leq i \leq m, 1 \leq j \leq n$

Output: Values for $x_1,...,x_n$ that min/max object function and satisfy all constraints.

Note: we cannot have non-linear things.

##### Corn Crop Problem

There are 2 types of corn crops, $C1$ that is used for human consumption and $C2$ used for animal feed.

Planting requires:

- labour
- seed
- pesticide

Profit:

- $C1$: $3/hec
- $C2$: $2/hec

Resources:

- $\leq 40$ hours of labour
- $\leq 100$ kg seed
- $\leq 10$ bags of fertilizer

C1 requires per hec: 2 hrs of labour, 1 kg seed, 1 bag pest

C2 requires per hec: 1 hr of labour, 3 kg seed, 0 bag pest

Variables: $x_1, x_2$: amount of hec to plant of $C1, C2$

Object function: max $3x_1 + 2x_2$

Subject to $2x_1 + x_2 \leq 40$ (labour), $x_1 + 3x_2 \le 100$ (seed), $x_1 \leq 10$ (pesticide), $x_1, x_2 \geq 0$

When we draw the feasible region, we get a complex polygon. 