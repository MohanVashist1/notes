# LEC 22

## Integer Linear Programs / 0-1 Linear Programs

integer LP = LP where solutions must be in $\mathbb{Z}$

0-1 LP = Integer LP where solutions must be in $\{ 0,1\}$

Both of these problems are NP-complete, no Polynomial Time Algorithm

Express minimum vertex cover as 0-1 Linear Program

<u>Input:</u> $G=(V,E)$ undirected

<u>Output:</u> minimum cardinality $V' \subseteq V$ such that every edge in $E$ has an endpoint in $V'$

<u>Variables:</u> $x_v$ for each $v\in V$ [$x_v = 1$ iff $v$ belongs to the minimum vertex cover]

<u>Objective Function:</u> minimum $\sum_{v\in V} x_v$ such that $x_v \in \{0,1\}, v\in V$ and $x_v +x_v \geq 1 | \forall \{u,v\} \in E$

## LP Duality

maximize $ c_1 x_1+ ...+c_n x_n$ such that

$a_{11} x_{1} + ... + a_{1n} x_{n} \leq b_1$

.

.

.

$a_{m1} x_{1} + ... + a_{mn} x_{n} \leq b_m$

$x_1,...,x_n \geq 0$

This is the <u>standard max form</u>

For example: consider the Linear Program (P)

max $3x_1 + 2x_2$ such that

$2x_1 + x_2 \leq 40$

$x_1 + 3x_2 \leq 100$

$x_1 \leq 10$

$x_1, x_2 \geq 0$

Note that $3x_1 + 2x_2 \leq 3x_1 + 9x_2 \leq 300$ Using the second constraint $\times 3$

Note that $3x_1 + 2x_2 \leq 4x_1 + 2x_2 \leq 80$ Using the first constraint $\times 2$

So we're looking for non-negative multipliers to multiply the constraint $y_1,y_2,y_3 \geq 0$ such that

$2y_1 + y_2 + y_3 \geq 3$

$y_1 + 3y_2 \geq 2$

These two constraints $(\star)$.

If $(y_1,y_2,y_3)$ satisfies $(\star)$, we get that

$3x_1 + 2x_2 \leq 40y_1 +100y_2 + 10y_3$, so we have an upper bound for the objective function

Now we want to minimize $40y_1 +100y_2 + 10y_3$ subject to $(\star)$, and that $y_1,y_2,y_3 \geq 0$. This is another linear program. We all this program (D). This is the <u>standard minimum form</u>

We have two linear programs, (P)rimal and (D)ual.

Note that the number of variables in the duals is equal to the number of constraints in primal

We can mechanically turn one linear program to another.

$\forall$ feasible solution $x=(x_1,x_2)$ of the P

$\forall$ feasible solution $y = (y_1, y_2, y_3)$ of the D

value of P @ x $\leq $ value of $D$ @ y

The gap between these two sets of values is called the <u>duality gap</u>.

If there exists a feasible $x^\star, y^\star$ solutions such that value of P @ $x^\star$ = value of D @ $y^\star$, then $x^\star, y^\star$ are optimal for P and D

For this example, lets take

$x=(x_1, x_2) = (4,32), y=(y_1, y_2, y_3) = (\frac{7}{5}, \frac{1}{5}, 0)$

the value of P @ x = 12 + 64=76

the value of D @ y = 56 + 20 = 76

For any linear program, the duality gap is always 0.

<u>Generally:</u>

We want multipliers $y_1,...,y_m$ such that

$a_{11} y_1 + ... + a_{m1}y_m \geq c_1$

.

.

.

$a_{1n} y_1 + ... + a_{mn}y_m \geq c_n$

So now we have that

$\sum^n_{j=1} c_j x_j \leq \sum^n_{j=1} \sum^m_{i=1} a_{ij} y_i \geq c_j = \sum^n_{j=1} \sum^m_{i=1} a_{ij} y_i x_j = \sum^m_{i=1} y_i \sum^n_{j=1} a_{ij} x_j \leq \sum^m_{i=1} b_iy_i$

So Objective function of P $\leq $ objective function of D

