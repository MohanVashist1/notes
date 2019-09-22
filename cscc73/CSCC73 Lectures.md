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

### LEC 3: Wednesday, September 11, 2019

#### Djikstra's Shortest Path Algorithm (KT 4.4, DPV 5.4)

<u>Note:</u> weights of path = sum of weights of edges of said path

<u>Input:</u>

- Weighted (di)graph $G = (V,E)$
- source node $s \in V$
- weight function on edges $wt: E \mapsto \mathbb{R}^{+}_0$

<u>Output:</u>

$$\forall v \in V, \delta(v) = \begin{cases} \text{min weight of any $s\rightarrow v$} \\ \infty, \text{if no $s\rightarrow v$ path exists} \end{cases}$$

Algorithm maintains a set of nodes $R \subset V$ which contains the "explored" region of the graph, and $\forall v \in V$, it maintains a quantity $d(v)$ such that:

1. $\forall v \in V, d(v) = \text{min weight of $s\rightarrow v$ path where all nodes that are not $v$ are in $R$}$
   1. We will call this an $R$-path
   2. If the $R$-path does not exist, $d(v) = \infty$
   3. $d(v) \geq \delta(v)$
2. $\forall v \in R, d(v) = \delta(v)$

Note that when $R$ becomes the entire graph, we will have what we wanted.

Algorithm:

- $R := \empty$
- $d(s) := 0$
- for each node $v\neq s$ do $d(v := \infty)$
- while $R \neq V$ do
  - $u :=$ node not in $R$ with min $d$- value
  - $R := R \cup \{ u \}$
  - for each node $v | (u,v) \in E$ do
    - if $d(v) > d(u) + w(u,v)$ then
      - $d(v) := d(u) + wt(u,v)$

Consider the graph of Nodes divided into two sets, $R$ and $V-R$. For each node $v$ in $V-R$, we check if our $d(v)$ is optimal after each iteration.

This algorithm calculates distance from the start node, but we need an algorithm to give us the shortest path, to know that, we keep track of the predecessor node in the path in an updated algorithm

Algorithm:

- $R := \empty$
- $d(s) := 0$
- $p(s) := $NIL
- for each node $v\neq s$ do $d(v := \infty)$
- while $R \neq V$ do
  - $u :=$ node not in $R$ with min $d$ value
  - $R := R \cup \{ u \}$
  - for each node $v | (u,v) \in E$ do
    - if $d(v) > d(u) + w(u,v)$ then
      - $d(v) := d(u) + wt(u,v)$
      - $p(v) := u$

where $p(s)$ is the predecessor of the node $s$.

We can find the shortest path by starting at the solution and then keep referring to the predecessor to work our way back.

Running Time: ($n = |V|, m=|E|$)

- "Naive" Implementation
  - Have array for $d$ values and nodes in $R$.
  - $O(n^2)$
- Heap Implementation for the node with minimum $d$ value
  - Initialize: $O(n)$ time
  - Place nodes in not in $R$ into the Heap: $O(n)$
  - $n$ EXTRACT MIN operations (which is $O(\log n)$)
  - $m$ CHANGEKEY operations (which is $O(\log m)$)
  - Total Running Time $O((n+m) \log n)$

Is the sophisticated implementation faster than "naive" implementation? Not really.

If we have a dense graph $m = \Theta(n^2)$ edges. Then the Naive Implementation is better.

If we have a sparse graph ($m=\Theta(n)$ or $\Theta(n\log n)$) Then the sophisticated implementation is better.

What graph represention should we use? Adjacency Matrix or Adjacency List?

Note that Dijsktra does not work if there are negative edges.

##### Correctness of Dijsktra

<u>Claim 1:</u> $d(v)$ is non-increasing

<u>Claim 2:</u> $d(u)$ does not change in the iteration when $u$ is added to $R$

<u>Claim 3:</u> if $d(v) = k \neq \infty$, there is an $s\longrightarrow v$ $R$-path of weight $k$

<u>Claim 4:</u> If $d(u) = \infty$ when $u$ is added to $R$, there is no $s\longrightarrow u$ path 

<u>Claim 5:</u> When $u$ is added to $R$, $d(u) = \delta (u)$

Claim 1 is trivial from looking at the algorithm. It is only reassigned when it is decreasing.

For Claim 2, this can change if $u$ has a negative self loop, but we're assuming that there are no negative weights, and Claim 2 works with that stipulation.

For Claim 3, it is true in every iteration, since in every iteration, we are adding another node.

For Claim 4. Suppose $u$ is added to $R$ in iteration $i$ and suppose $d_i(u) = \infty$. Let $j$ be the earliest iteration in which some node $x$ is added to $R$ with $d$-value = $\infty$. We know that $1 < j \leq i$. $\not\exists $ edge $(x,y)$ such that $x\in R_{j-1}$ and $y \not\in R_{j-1}$

We will prove the last statement by contradiction.

Suppose for contradiction such edge $(x,y)$ exists.

Let $j'$ be the iteration $x$ was added to $R$. $j' \leq j = 1$. Because of that, we know that $d_{j'} (x) \neq \infty$ because the first iteration in which $d(x)$ was infinity was $j$. This implies that when $x$ was inserted into $R$, $y$ was not infinity at $j'$, and that $y$ was also not infinity at $j$ since $j' < j$.

We have a contradiction as $y$ is not in $R$ but it has a not infinity $d$-value. This is contradictive to the definition of $j$. Therefore Claim 4 is true.

Therefore, there is no $s\longrightarrow u$ path, because otherwise the contradiction in claim 4 would work, and it does not.

For Claim 5, we will use complete induction:

We will assume this is true for all nodes added to $R$ before iteration $i$. We will show it is true for nodes $u$ added to iteration $i$.

$i = 1, s \in R$ and $d(s)$ = 0, which is correct.

$i > 1$, if $d(u) = \infty$ when $u$ is added to $R$, done by previous claim. It remains to show for when $d(u) \neq \infty$.

If $d_i(u) \neq \infty$ then by claim 3, there exists $s\rightarrow u$ $R$-path of weight $d_i(u)$ and $d_i (u) \geq \delta (u)$. 

We want to prove that this path is the shortest path. Consider the shortest $s \rightarrow u$ path $P$ with weight $\delta (u)$. This shortest path $P$ must cross out of $R$ where $x$ is the node inside $R$ (inserted at iteration $j$) and $y$ is the consecutive node outside of $R$.

$d_i(u) = d_{i-1} (u)$ [by claim 2]

$d_i(u) = d_{i-1} (u) \leq d_{i-1} (y)$ [by the choice of $u$ in the algorithm]

$d_i(u) = d_{i-1} (u) \leq d_{i-1} (y) \leq d_j (y)$ [$j$ is the iteration when $x$ was added to $R$, so we know that $j \leq i - 1$, and this is true by claim 1]

$d_i(u) = d_{i-1} (u) \leq d_{i-1} (y) \leq d_j (y) \leq d_j(x) + wt(x,y) $ [by the algorithm]

$d_i(u) = d_{i-1} (u) \leq d_{i-1} (y) \leq d_j (y) \leq d_j(x) + wt(x,y) = \delta (x) + wt(x,y) $ [This is true because $j \leq i - 1$, and according to the induction hypothesis].

$\delta (x) + wt(x,y) = wt(\text{Prefix of $P$ up to $x$} + wt(x,y))$ [because $P$ is a shortest path]

$wt(\text{Prefix of $P$ up to $x$} + wt(x,y) \leq wt(P)$ [Since edge weights are all 0 or more]

$wt(P) = \delta(u)$ by the defintion. So $d_i(u) \leq \delta(u)$.

<u>Theorem:</u> When the algorithm ends, $d(v) = \delta(v), \forall v \in V$. We know this because of Claim 5 and 3.

###  LEC 4: Monday, September 16, 2019

#### Huffman Codes (DPV 5.2, KT 4.8)

Alphabet $\Gamma$ = finite set of symbols

string over $\Gamma$ = text

$n = |\Gamma|$

Code for $\Gamma$: map each $a\in \Gamma$ to binary string (code word for the symbol $a$)

- fixed length $\longrightarrow \lceil log_2 |\Gamma| \rceil$
- variable length

Note that fixed length feels wasteful as letter frequencies are different. We should give frequent letters short codes and infrequent letters long codes, thus, variable length codes.

However, we should be careful, because consider <u>the code:</u>

$A \longrightarrow 1$

$B \longrightarrow 01$

$C \longrightarrow 010$

Then with this code, $0101$ can either be $BB$ or $CA$, which we don't like.

So we'll use <u>Prefix Codes</u>: where no codeword is a prefix of another. This helps make decoding unambiguous, and this will appeal to us as we can represent any prefix binary code as a binary tree.

$$\Gamma = \{ A,B,C,D,E,F \}$$

We place the symbols as the leaves in a binary tree, we consider every left edge as 0 and right edge as 1, and so each symbol is representated from the path from the head to the corresponding leaf. This tree representation prevents us from using a symbol's representation as a prefix for another.

<u>Input:</u> Alphabet $\Gamma, n = |\Gamma|$

$\forall x \in \Gamma, f(x)=$ frequency of $x$ and that $\sum_{x\in\Gamma} f(x) = 1$

<u>Output</u>: Binary tree $T$ represents optimal prefix for $\Gamma$

minimizing $AD(T) = \sum_{x \in \Gamma} f(x) \cdot depth_T(x)$ where $AD(T) =$ Average Depth of the tree $T$ and $depth_T(x) = $ depth of a leaf for symbol $x$ in tree $T$.  

Then our $AD$ will be the weight of our Huffman Tree. We can optimize it by placing higher frequency leaves at lower depth leaves.

<u>Fact 1:</u> An optimal tree must be full (internal nodes have 2 children).

If we consider the case where there exists a tree with a left child (for example), but no right child, then all the nodes in the left child tree have this 0 in front of it that isnt differentiating it from a right child since the right child doesnt exist, so we can get right of the 0 edge.

<u>Fact 2:</u> In an optimal tree $T$, $f(x) > f(y) \longrightarrow depth_T(x) \leq depth_T(y)$ (higher frequencies means lower or equal to depth) 

Both Fact 1 and 2 imply that if $x,y \in \Gamma$ are symbols with minimum frequency $\longrightarrow \exists$ an optimal tree such that $x,y$ are siblings and are leaves at max depth.

Now consider the following.

If we have two siblings $x,y$, then we can consider its parent as a "super symbol" that has a frequency of $f(x) + f(y)$ and if we recursively do this by lining up the symbols by their frequency, we produce a Huffman Tree. This is Huffman's Algorithm.

<u>Note:</u> Algorithm may result in different trees (ie. codes) all of them are optimal.

<u>Proof of Algorithm</u>: We will use induction on the size of the alphabet $n$.

Assume tree produced by algorithm on inputs of size $n$ is optimal, we want to prove that it is optimal for $n+1$.

Input: $\Gamma$ alphabet, $f$ frequencies, $|\Gamma| = n+1$

Let $H$ be the tree resulting by running the algorithm on ($\Gamma$, $f$). Let $x,y$ : be two symbols with frequency that are siblings in $H$.

Lets now consider $\Gamma' = (\Gamma - \{x,y\}) \cup \{ z \}$ where $z$ is a new symbol.

So now $f'(a) = \begin{cases} f(a), a\neq z\\ f(x) + f(y), a = z \end{cases}$

$H'$, which is the result of the algorithm on the input $\Gamma'$ , $f'$. This is optimal by the induction hypothesis

Now let us consider $T$, which is an optimal tree for $\Gamma, f$. We can assume without loss of generality that $x,y$ are siblings at maximum depth. We will now do onto $T$ to get $T'$ what we did to $H$ to get $H'$.

So $T'$ has the $x,y$ tree turned into a $z$ leaf, and we know it is some tree for $\Gamma', f'$.

$= AD(H)$

$= AD(H') + f(x) + f(y)$, note that $H'$ is optimal by our Induction Hypothesis

$\leq AD(T') + f(x) + f(y)$ because $H'$ is optimal.

$= AD(T)$ this is optimal by assumption.

