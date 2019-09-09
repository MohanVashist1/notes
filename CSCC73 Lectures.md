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

### LEC 2: Monday, September 9, 2019

- A1 Posted

#### Minimum-Maximum Lateness Scheduling (KT 4.2)

<u>Input:</u>

- $n$ jobs $1,2,..., n$
- a release time $r$
- for each job $i$
  - $t(i)$ = duration of $i$
  - $d(i)$ = deadline of $i$

We want to minimize the amount of time we have missed the deadline.

A <u>Schedule:</u> $s: i \mapsto s(i)$, where $s(i) \geq r$ (is a mapping from jobs to start time), specifies time when job $i$ is to start such that $\forall i, j$ where $i \neq j$ we have $[s(i), s(i)+d(i)]$ and  $[s(j), s(j)+d(j)]$ do not overlap.

The Lateness of job $i$ in schedule $s$ is defined as $l(s,i) = max(0, s(i)+t(i)-d(i))$

The maximum lateness of $s$ is $$max_{1 \leq i \leq n} l(s,i)$$

$r$ is essentially when the schedule starts

<u>Output:</u>

The output is the schedule of minimum lateness as we have defined it.

Example:

$r = 0, n = 4$

$t(a) = 4, d(a) = 5$

$t(b) = 3, d(b) = 3$

$t(c) = 2, d(c) = 8$

$t(d) = 1, d(d) = 2$

A possible schedule $s$ can be $s(d) = 1, s(a) = 3, s(b) = 7, s(c) = 11$

The lateness of this schedule is 7

| $l(s,i)$ | $i$  |
| -------- | ---- |
| 2        | a    |
| 7        | b    |
| 5        | c    |
| 0        | d    |

Another possible schedule $s$ can be $s(d) = 0, s(a) = 1, s(b) = 5, s(c) = 8$

The lateness of this schedule is 5

| $l(s,i)$ | $i$  |
| -------- | ---- |
| 0        | a    |
| 5        | b    |
| 2        | c    |
| 0        | d    |

<u>Fact 1:</u> There is an optimal schedule with no gaps in it

Another possible schedule $s$ can be $s(d) = 0, s(a) = 4, s(b) = 1, s(c) = 8$

The lateness of this schedule is 3

| $l(s,i)$ | $i$  |
| -------- | ---- |
| 3        | a    |
| 1        | b    |
| 2        | c    |
| 0        | d    |

This schedule is actually optimal for this set of jobs.

How should we sort these jobs? Brute force is $O(n!)$, so let's find a greedy way.

We'll first try to sort the jobs by **increasing deadline first**

Our algorithm outline will look like this

- Sort jobs in increasing deadline
- let $d[1...n]$ be deadlines of the sorted jobs
- let $t[1...n]$ be durations of the sorted jobs
- $F := r$ # finish of last job scheduled
- for $i := 1$ to $n$ do
  - $gs(i) :=F$
  - $F := F + t(i)$
- return $gs$

The running time of this algorithm is $\theta (n\log n)$

<u>Invariant:</u> $gs$ is a schedule with no gaps of the first $i$ jobs **(in increasing deadline)**

<u>Definition:</u> An **Inversion** in the schedule $s$ is a pair of jobs $i, j$ such that $s(i) < s(j)$ but $d(i) > d(j)$

<u>Fact 2:</u> All Schedules with no gaps and no inversions have the same lateness

<u>Theorem:</u> Every schedule with no gaps and no inversions is optimal.

The maximum number of inversions any schedule can have is $n^2$, just a fun fact

<u>Proof for Theorem:</u> We'll do this by contradiction.

Let $s$ be an optimal schedule with no gaps and at least one inversion

$\longrightarrow$ We're assume that $s$ has an inversion involving two successive jobs $i, j : s(j) = s(i) + t(i)$

or the inversion can be between non-successive jobs, like such:

$i'\rightarrow\rightarrow\rightarrow i\rightarrow j\rightarrow\rightarrow j'$ where $d(i') > d(j')$ and $d(i) < d(j)$

So we'll find a pair $i,j$ either way

consider the case where we swap $i,j$, we'll call this new schedule $s'$

Observations:

- $s'$ has fewer inversions than $s$.
- All jobs that are not $i,j$ have the same lateness in $s'$ and $s$
- $l(j, s') \leq l(j, s)$, this is good
- $l(i, s') \geq l(i, s)$, this is bad
- However, $l(i, s') \leq l(j, s)$, so the maximum lateness of any job in $s' \leq$ the maximum lateness of any job in $s$

