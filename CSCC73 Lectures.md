# CSCC73

## Lecture Notes

### LEC 1: Wednesday, September 4, 2019

Outline

- Greedy Algorithms
- Divide-and-conquer Algorithms
- Dynamic Programming Algorithms
- Maximum Flow Problem
- Linear Programming

Course Webpage: http://www.cs.toronto.edu/~vassos/teaching/c73/

Assignments are done in groups of two

#### Greedy Algorithms (KT 4, DPV 5)

Optimization Problems: Given an input, find an output ("solution") that has two properties:

- The solution satisfies certain **constraints** (the solution must be "feasible")
- The solution optimizes (minimizes or maximizes, depending on the context) a **desired criterion** (the solution must satisfy the objective function)

**For example**: Mininum Spaning Trees. The Input is a Graph, the Output is a graph that is a spanning tree that minimizes the sum of the weights of the edges.

We will be looking at Interval Scheduling, which takes a set of intervals, and outputs a set of intervals where the set contains the most amount of intervals, with the constraint that they don't intersect.

A Greedy Algorithm:

- Builds a solution incrementally
- At each stage, it has constructed a partial solution and extends it to a more complete solution.
- It does this <u>greedily</u> and <u>irrevocably</u>.
  - Greedy, meaning "the one with the best score" for some criteria
  - Irrevocably, meaning no back-tracking

Sometimes Greedy Algorithms work, sometimes they don't.

NP-Complete Problems exist in which it is difficult to find the optimal solution, some of the algorithms that find approximate solutions (somewhat good solutions) are greedy algorithms. So the greedy method can solve a lot of problems.

#### Interval Scheduling (KT 4.1)

<u>Input:</u> $n$ intervals ("jobs" or "tasks"), labeled $1,2,..., n$.

Each interval $i$ has start time $s(i)$ and finish time $f(i)$ where $f(i) > s(i)$

So an interval $i$ is $[s(i), f(i)]$

Intervals $i$ & $j$ overlap (or "conflict") if the set $[s(i), f(i)] \cap [s(j), f(j)]$ contains more than one point in it.

A set of intervals is **feasible** if no two intervals in the set overlap.

<u>Output:</u> A maximum Cardinality feasible subset of the input.

One solution is bruce force, which is not very fast. We can do better with a greedy algorithm.

<u>Greedy Algorithm Outline:</u>

- sort interval in "some order"
- $A = \emptyset$
- for each interval $i$ in sorted order, do
  - if $i$ overlaps no interval in $A$ then
    - $A = A \cup i$
- return $A$

<u>Strategy A:</u> the "some order" will be sorting by start time.

This results in a feasible set, but is it optimal?

<u>Counter-Example for A:</u> consider $\{ i, j, k\}$ where $s(i)=1, f(i)=99$

and $s(j), s(k), f(j), f(k) \in [s(i),f(i)]$, this means that only $\{i\}$ is picked, but the optimal solution $\{j,k\}$

<u>Strategy B:</u> sort by the length of the interval, from shortest to longest

<u>Counter-Example for B:</u> What if there is a small interval that conflicts with two intervals, in which the two intervals together without the small interval is optimal? Then the algorithm will pick the small interval, and it is not optimal.

<u>Strategy C:</u> sort by number of conflicts

<u>Counter-Example for C</u>: There exist an arrangement in which the optimal intervals are not the intervals with the least number of conflicts, so they might not be chosen.

<u>Strategy D:</u> sort by finish time.

The intuition behind this is that the interval chosen gives the most amount of time to fit in other intervals, so to not take too much "space". To pick a job that finishes the earliest.

Algorithm for Strategy D:

- sort intervals by finish time
- $A := \emptyset$
- $F := -\infty$
- for each interval $i$ in sorted order, do
  - if $i$ overlaps no interval in $A$ or $(s(i) \geq  F)$ then
    - $A := A \cup i$
    - $F := f(i)$
- return $A$

Now lets prove that Strategy D outputs an optimal set.

<u>Proof of optimality</u>

<u>Claim 1.</u> $A$ is a feasible set. We won't prove this because $A$ is feasible in every step of the algorithm, and thus, results in a feasible set (it is trivial).

Because $A$ is feasible, we can look at the intervals in $A$ from left to right, labeled $j_1, j_2, ..., j_k$ in left to right order, which is also the order of insertion into A.

Let $j^*_1, j^*_2, ... , j^*_m$ be intervals in any optimal set $A^*$ in left to right order.

<u>N.B.</u> We know that $k \leq m$, because $m$ is the maximum number of intervals in a feasible set.

<u>Claim 2.</u> $f(j_t) \leq f(j^*_t), t = 1,2,..., k$

Note that the greedy solution always "stays ahead".

<u>Proof:</u> By induction.

<u>Basis:</u> $k=1$, this is trivial as the greedy algorithm selects the interval that finishes first.

<u>Induction Step:</u> lets assume the Induction Hypothesis is true for $t$. Assume it is not true for $t+1$.

However, since $f(j_t) \leq f(j_t^*)$, and if $f(j_{t+1}) \geq f(j^*_{t+1})$, then we have a contradiction, since the greedy algorithm should have chosen $j^*_{t+1}$ instead of $j_{t+1}$ to insert into $A$ since $j_{t+1}$ finishes before $j^*_{t+1}$ and does not conflict with $j_t$ since $f(j_t) \leq f(j^*_t) \leq s(j^*_{t+1}) \leq f(j^*_{t+1})$, so $j_{t+1}^*$ is still available to be picked and the algorithm should have picked it. $j_{t+1}^*$ also has priority over $j_{t+1}$ so the algorithm should not have chosen $j_{t+1}$ for the $t+1$th interval. So we have a contradiction here. Therefore it must be true for $t+1$.

<u>Claim 3.</u> $k=m$. Recall that $k \leq m$. If $k \neq m$ then $k < m$

That means $j^*_{k+1}$ exists and that  $f(j_{k}) \leq s(j^*_{k+1}) \leq f(j^*_{k+1})$. So the greedy algorithm should have added $j^*_{k+1}$ to $A$, but it did not. This is a contradiction.

Thus, we have proved that our solution is optimal.

We also have another technique to prove this.

The "Promising set" technique.

<u>Invariant:</u> At the end of each iteration $t$, $A_t$ is contained in some optimal set $A^*$ ($A_t$ is the set contain in the variable $A$ at the end of iteration $t$).

So $A_t \subseteq A^*$ for every $t$. This is what we're trying to prove.

So we'll solve this by induction.

Assume this works for iteration $t$, let us now consider iteration $t+1$

(Nevermind he doesn't solve it in lecture but links to something on the course webpage)

There are also other problems similar to this like:

- Weighted Interval Scheduling