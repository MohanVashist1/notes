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
- $p(s) := $ NIL
- for each node $v\neq s$ do $d(v) := \infty$​
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

### LEC 5: Wednesday, September 18, 2019

#### Divide and Conquer (KT 2, DPV 5)

<u>Merge Sort</u> -  To sort an array $A$ of $n$ items $(a = b = 2)$

- if $n = 1$, trivial
- else
  - split into two $\frac{n}{2}$ subarrays
  - sort each subarray
  - merge sorted subarrays

<u>Binary Seach</u> Searching a sorted array $A[1...n]$ $(a = 1, b = 2)$

- if $n=1$, trivial
- else if $A[\frac{n}{2}] \geq$ element (ceiling) is what we are looking for 
  - then we recursively search $A[1... \frac{n}{2}]$
  - else we recursively search $A[\frac{n}{2} ... n]$

To solve an instance of size $n$ of some problem:

- if $n$ is "small", solve directly
- else
  - split input into some $a$ pieces, each of size $\frac{n}{b} $($a \geq 1, b > 1$ are constants)
  - recursively solve each subproblem (each of size $\frac{n}{b}$)
  - combine solutions to subproblems of original instance (of size $n$)

With this recursion, we're reducing the input size by a factor of $b$ at each call, rather than by a constant. i.e.

$$n \longrightarrow n-c \text{ vs. } n\longrightarrow \frac{n}{2}$$

This means that the depth of recursion for divide and conquer algorithms is $\Theta (\log n)$.

Our Divide and Conquer Algorithms will reduce the input size to $\frac{n}{b^{\log_b n}} = 1$ (assuming $n$ is a power of $b$). There are $a^{\log_b n} = n^{\log_b a}$ subproblems of size 1.

Generally, Divide and Conquer running times look like such:

$T(n) = a \cdot T(\frac{n}{b}) + c \cdot n^d$

$T(1) = c$

Where $a$ are the recursive calls, $b$ is how much the input is divided by and $d$ is the amount of work that is done every recursion.

**Master Theorem:** Solution to

$T(n) = a \cdot T(\frac{n}{b}) + c \cdot n^d$

$T(1) = c$

- (a) if $a < b^d$ then $T(n) = \Theta (n^d)$ 
- (b) if $a = b^d$ then $T(n) = \Theta (n^d \log n)$ 
- (c) if $a > b^d$ then $T(n) = \Theta (n^{\log_b a})$ 

The intuition is that we're count how many time we need for each step.

For recursive call $i$, it takes $a^i \cdot c \cdot (\frac{n}{b^i})^d$

So we can represent this as a sum:

$T(n) = cn^d \sum^{\log_b n}_{i = 0} (\frac{a}{b^d})^i$

Consider $G(n) = \sum^{\log_b n}_{i = 0} (\frac{a}{b^d})^i$

Remember that $\sum^k_{i=0} x^i = \frac{x^{k+1} - 1}{x-1} $

And that $x \in (0,1) | \sum^\infty_{i=0} x^i = \frac{1}{1-x}$

Lets consider each case where $T(n) = cn^d \cdot G(n)$

<u>case $(a)$:</u> $a < b^d$

$G(n) = \sum^\infty_{i = 0} (\frac{a}{b^d})^i = \frac{1}{1-\frac{a}{b^d}} \leq k | k \in \mathbb{z}$

So $T(n) = \Theta (cn^d \cdot k) = \Theta (n^d)$

<u>case $(b)$:</u>  $a = b^d$

$G(n) = 1 + \log_b n = \Theta (\log_b n)$

So then $T(n) = \Theta (n^d \log n)$

<u>case (c):</u> $a > b^d$

So we know that the series does not converge

So $G(n) = \frac{(\frac{a}{b^d})^{1 + \log_b n} - 1}{\frac{a}{b^d} -1} = \Theta (\frac{a}{b^d})^{\log_b n}$

 $(\frac{a}{b^d})^{\log_b n} = \frac{a^{\log_b n}}{(b^{log_b n})^d} = \frac{a^{\log_b n}}{n^d}$

So $G(n) = \frac{a^{\log_b n}}{n^d}$

So $T(n) = \Theta (a^{\log_b n}) = \Theta (n^{\log_b a})$



### LEC 6: Monday, September 23, 2019

#### Closest pair of points (KT 5.4, DPV 2.32)

<u>Input:</u> Set $P$ of $n$ points on the plane, each point $p = (x,y) \in P$

The Distance between $p=(x,y)$ and  $p'=(x',y')$ is euclidean, i.e. $d(p, p') = \sqrt{(x-x')^2 + (y-y')^2}$

<u>Output:</u> A pair of points $(p,p')$ in $P$ no farther apart than any other two points. $\forall q,q' \in P, d(p,p') \leq d(q,q')$

Let us first consider the one dimension version of this, we dont have to compare each point to every other, we just have to compare each point to their neighbours. We can say that $T(n) = 2 T(\frac{n}{2})+c$, so $a=2, b=2, d=0$, and since $2 > 2^0$ Then $T(n) = \Theta (n^{\log_2 2})$

So, consider a bunch of points, the algorithm would be splitting the points into 2 groups, and finding the two closest points in the two groups, with distance $\delta_L, \delta_R$. We will consider the $m$ point, which separates the left from the right, and consider the band $B$ which is on $m$ with a distance of $\delta = min(\delta_L, \delta_R)$ on both the left and right side. We can now focus on the band.

Let us now focus on some point $x$ on the bottom (we'll consider them in increasing $y$). We do not need to compare $x$ with all of the points on the other side, but the next 7 points on the other side (will be explained later).

To find the clostest pair of points in $B$ that are less than $\delta$ apart, it suffices to consider, for each point in $B$, only the "next" 7 points above that point (greater $y$ coordinate).

<u>Claim:</u>

 Let $p,q \in B, p\neq q$. If $d(p,q) < \delta$, then $\exists \leq 6$ points other than $p,q \in B$ whose $y$-coordinates are between $p$'s and $q$'s.

<u>Proof:</u> Assume for contradiction that this is false, so we assume that $\exists \geq 7$ points between $p=(x,y)$ and $q=(x',y')$. Without Loss of Generality, assume $y \leq y'$.

Consider $p$ on one side. $q$ cannot be on the same side because then it would get picked up by our recursion. $q$ cannot be on the other side outside of the $\delta$ box as it is already further than $\delta$, and we're looking for two points shorter than $\delta$. Therefore since we have 9 points including $p,q$ and 7 other points, which must be in two boxes. We can say that one box must hold at least 5 points

So in this one box with at least 5 points, we can split the box into quarters of $\delta/2$. We have 5 points for $4$ quarters of the box, so by pigeonhole principle, one box must contain 2 points. The max distance two points can be in the box is $\frac{\sqrt{2}\delta}{2}$. This is a contradiction, since we stated that $\delta$ was the shortest distance between any two points bween any two points, and $\delta > \frac{\sqrt{2}\delta}{2}$ .

Algorithm is another sheet online.

<u>Running Time:</u> $T(n) = 2 T(\frac{n}{2}) + n$, $a=2, b=2, d=1$ so $T(n) = \Theta(n\log n)$

Fun practice problem: Toronto has acquired a new park that is 35 by 35 meters, and someone decided to plan 50 trees. Someone then decides that the trees need to be at least 7.5 meters apart. You must prove that it cannot be done.

### LEC: Monday, September 30, 2019

#### Fast Fourier Transform (FFT) (DPV 2.6, KT 5.6)

Suppose we have two polynomials of degree $m$.

$A(x) = a_0 + ... + a_m x^m$

$B(x) = b_0 + ... + b_m x^m$

$C(x) = B(x) \cdot A(x) = c_0 + ... + c_{2m} x^{2m}$

Note that:

$c_0 = a_0 + b_0$

$c_1 = a_1 b_0 + a_0 b_1$

$c_2 = a_2 b_0 + a_1 b_1 + a_0 b_2$

....

$c_{2m} = a_m b_m$

So essentially, $c_k = \sum_{1 \leq i,j \leq m | i + j = k} a_i b_j$

The number of operations to compute $c_k$s are $\Theta (1+2+...+m+(m+1) +m+ m-1 + ... +1) = \Theta (m^2)$

Note: This is <u>Convolution</u>

$(a_0, ..., a_m) \star (b_0 ,...,b_m) = (c_0, ..., c_{2m})$

This is used for signal processing. A signal is just a vector that we pass through a filter.

We can represent polynomials as coefficient vectors in the coefficient representation of the polynomial, we can also use a value representation of the polynomial.

<u>Interpolation Theorem:</u> A polynomial of degree $m$ is uniquely determined by its value at $m+1$ points.

We have seen interpolation before. Given 2 points, we can draw a unique line connecting them, given 3 points, we can draw a parabola, etc.

Coefficient representation of $A(x) = a_0,a_2,...,a_m$

Value representation of $A(x) = A(x_0),A(x_1), ..., A(x_m)$

**Evalution** is going from Coefficient $\longrightarrow$ Value

### LEC: Monday, October 7, 2019

#### Dynamic Programming (KT, DPV Ch 6)

Consider the Longest increasing subsequence (LIS) problem.

A **subsequence** of a sequence $A = a_1, a_2, ..., a_n$ is a sequence $a_{i_1}, a_{i_2}, ..., a_{i_k} | 1 \leq i_1 < i_2 < ... < i_k \leq n$

<u>Input:</u> A sequence $A = a_1, a_2, ..., a_n$  of numbers

<u>Output:</u> A LIS of A (length of LIS of A) (there are multiple so we just want any)

To solve this, we want to look "backwards"

Assume we are given a LIS of A, say S. $S = S', a_i$ ($S$ is built from $S'$). So $S$ ends with $a_i$ at position $i$ of $A$. So we claim that $S'$ is a longest, increasing subsequence at $A$, ending at some position $j | j < i$ and $a_j < a_i$

But suppose, for contradiction, $\exists S'' | S''$ is an

- increasing subsequence of $A$ ending in position $k$
- such that $k < i$ and $a_k < a_i$
- $|S''| > |S'|$

Look at $S'', a_i$.

This is called a "cut-and-paste" argument.

So we found the "optimal substructure" of this problem. This means that the optimal solution to the problem is an optimal solution to some subproblem, extended.

This sounds like all problems, but some problems don't have this. Like finding the cheapest flight which may not have optimal solutions to sub problems due to airline loyalty programs.

The Length of LIS ending at position $i$ = The Lenfth of LIS ending at some position $j | j < i$ (with $a_j < a_i$). Which $j$? Don't know, try them all, use the best.

<u>Definition:</u> $L(i) = $ length of LIS of $A$ ending at position $i$. (Definition $\star$)

How to compute $L(i)$?

$L(i) = \begin{cases} 1, \text{if $a_i <a_j$ for all $j | 1 \leq j < i$}\\ \text{max}\{L(j) + 1 : 1 \leq j < i \text{ and } a_j < a_i \} \end{cases}$ (Definition $\dagger$)

LongestIncreasingSubsequence$(A)$

- for $i := 1$ to $n$ do
  - $L(i) := 1$
  - $\text{pre}(i) := 0$
  - for $j := 1$ to $i-1$ do
    - if $a_j < a_i$ and $L(j) + 1 > L(i)$ then
      - $L(i) := L(j) + 1$
      - $\text{pre}(i) := j$
- return $L(\text{argmax}(L))$

But aren't $\star$ and $\dagger$ different?

We will show that they are the same. We will rename $\star L(i)$ to $L'(i)$

The steps for Dynamic Programming

1. Define a polynomial number of subproblems (from whose solution we can "easily" find the solution to our problem)
2. Devise a recursive formula to compute the subproblems.
3. Derive a solution to original problem from solutions to subproblems.

### LEC: Monday, October 21, 2019

#### Optimal Binary Search Trees

Records with keys $1,2,...,n$

$P(i) =$ probability of searching for key $i$.

<u>Use linked list:</u> $c(L) = \sum^n_{i = 1} P(i)\cdot \text{position}(L,i)$

A binary search tree has $\frac{2n\choose n}{n+1}$ of combinations

We want a tree that minimizes $c(T) = \sum^n_{i=1} P(i) \cdot (\text{depth}(T,i) + 1)$

We can try inserting nodes in a tree by their $P(i)$ value, but this is not optimal because if the last/first value has the highest probablity, only one side is used in the tree.

Maybe we should try to make a tree that is balanced? That doesn't work, we need to do Dynamic Programming

Suppose $T$ is an optimal BST for $1,2,...,n$ with left and right trees $T_L, T_R$ and the head has a value of $k$

What can we say about the subtrees? $T_L, T_R$ are both binary search trees and that $T_L$ contains values from $1...k-1$ and $T_R$ contains values from $k+1...n$. They are also optimal. Let's prove this.

Fact: $c(T) + c(T_L) + c(T_R) + \sum_{u\in T} P(u)$ because

$\begin{align*}c(T) &= \sum^n_{i=1} P(i) \cdot (\text{depth}(T,i) + 1)\\&= P(k)\cdot 1 + \sum_{i \in T_L} P(i) \cdot (depth(T,i) +1) + \sum_{i \in T_R} P(i) \cdot (depth(T,i) + 1) \\ &= \sum_{u\in T} P(u) + c(T_L) + c(T_R) \end{align*}$

Subproblems to solve: Find optimal BST for $i...j$, $1 \leq i \leq j \leq n$, call it $T_{ij}$

For $T_{1n}$ we need $T_{1,k-1}$ and $T_{k-1,n}$, but we need more, we need all $T_{ij}$ where the head is $i$ to $T_{ij}$ where the head is $j$.

$C[i,j]=c(T_{ij}), 1 \leq i \leq j \leq n$

$C[i,j] = \min_{i \leq k \leq j} C[i, k+1] + C[k+1, j] + \sum_{i \leq u \leq j} P(u)$

Compute with increasing $j-i$ + 1. This is the size of the problem (number of nodes in the tree).

### LEC 16: Monday, November 4, 2019

#### Max Flow and Applications (KT 7, DPV 7.2)

A Flow Network $\mathcal{F}(G,s,t,c)$

$G = (V,E)$ is a directed graph

$s,t \in V$

$c : E \mapsto \mathbb{R}^+_0$

$G$ has no edges into $s$ and no edges out of $t$.

Flow $f$ in $\mathcal{F}$: $f : E \mapsto \mathbb{R}^+_0$ such that:

- $\forall e \in E, 0 \leq f(e) \leq c(e)$ [capacity constraint]
- $\forall v \in V - \{ s,t \}, \sum_{e \in out(v)} f(e) = \sum_{e \in in(v)} f(e)$ [conservation constraint]

where $out(v) = \{ (v,u) : (v,u) \in E \}$ and $in(v) = \{ (u,v) : (u,v) \in E \}$

Value of flow $f$: $V(f) = \sum_{e \in out(s)} f(e)$

##### Max Flow Problem

<u>Input:</u> Flow network $\mathcal{F} = (G,s,t,c)$

<u>Output:</u> Flow $f$ in $\mathcal{F}$ of max value. $\forall$flow $f'$ in $\mathcal{F}$ , $V(f) \geq V(f')$

##### Min Cut Problem

Cut of flow net $\mathcal{F} = (G=(V,E), s,t,c)$:

$S, T \subseteq V | s \in S, t \in T, S \cap T = \empty, S \cup T = V$

capacity of cut $(S,T) = c(S,T) = \sum_{u \in S, v \in T} c(u,v)$

<u>Input:</u>  $\mathcal{F}$

<u>Output:</u> Cut $(S,T)$ of minimum capacity

$\forall$cut $(S', T')$ of $\mathcal{F}, c(S,T) \leq c(S',T')$

Max Flow = Min Cut

<u>Algo for improving flow</u>

- Found simple $s\to t$ path [ignore direction]
- increased flow through edges traversed in forward direction by $(b \leq c(e)-f(e))$ 
- decreased flow through edges traversed backward by $(b \leq f(e))$

### LEC 17: Wednesday, November 6, 2019

We will be looking at residual graphs today

Residual Graph $G_{f'}$ with respect to flow $f'$. Every edge is replaced with two edges, one going in the same direction and another going in the reverse direction, This represents the capacity that can be pushed or reversed, if an edge has 0, then we don't write it.

Given flow $f$ in flow network $F = (G,s,t,c), G=(V,E)$ the residual graph $G_f$ with residual capacities $c_f$. $G_f = V, E_f$ where 

- for every edge $(u,v)$ such that $f(u,v) < c(u,v)$ we put edge $(u,v)$ with residual capacity $c_f (u,v) = c(u,v) - f(u,v)$ in $E_f$ [forward edge]
- for everg edge $(u,v)$ such that $f(u,v) > 0$ we put edge $(v,u)$ with residual capacity $c_f (v,u) = f(u,v)$ in $E_f$. [backward edge]
- All residual capacities are strictly positive

augment($f$ = flow, $p$ = simple $s\to t$ path in $G_f$) [augmenting the graph]

- $b :=$ min res cap of any edge on $p$
- for each edge $(u,v)$ on $p$
  - if $(u,v)$ is a forward edge then $f(u,v) = f(u,v) + b$
  - else $f(v,u) = f(v,u) -b$
- return $f$

The returned $f$ of this function is an improved flow. We will prove this.

If $f$ is a flow and $p$ is a simple $s\to t$ path in $G_f$ then $f'$ = augment$(f,p)$ is a better flow. (better meaning that $V(f') > V(f)$). To prove that $f'$ is a flow, we need to show that it satisdies the capacity constraint and the conservation constraint.

**capacity constraint**: the concern is that we have either increased the flow to above the capacity or decreased the flow to below 0.

if $(u,v)$ is a forward edge, then 

$\begin{align*}f'(u,v) &= f(u,v) + b\\ &\leq f(u,v) + c_f (u,v)\\ &= f(u,v) + c(u,v) - f(u,v) \\ &= c(u,v) \end{align*}$

So this is safe.

if $(u,v)$ is a backward edge, then

$\begin{align*} f'(v,u) &= f(v,u) - b \\ &\leq f(v,u) - c_f(u,v) \\ &= f(v,u) - f(v,u) \\ &= 0\end{align*}$

So this is safe as well.

**conservation constraint:** $p$ in $G_f$ starts at $s$, goes to $t$, we may have messed up the conservation constraint, so let's check it.

For every node $v \neq s,t$ the paths in front or behind are either forwards or backwards, we'll prove that in all cases, the conservation constraing holds.

Forward, Forward preserves the constraint

Forward, Backward preserves the constraint

Backward, Forward preserves the constraint

Backward, Backward preserves the constraint

Therefore, we proved that our augmenting step produces a better flow.

#### Ford-Fulkerson Max Flow Algorithm

FF($F$ = $(G, s,t, c)$)

- for each edge $(u,v)$ of $G$ do $f(u,v) = 0$
- construct $G_f$
- while $G_f$ has an $s\to t$ path do
  - $p :=$ any simple $s\to t$ path in $G_f$
  - $f := $agument$(f,p)$
  - update $G_f$
- return $f$

1. Does this algorithm terminate?
2. Is this algorithm correct?

We will assume our capacities are integers, as irrational capacities may not terminate.

Observe.

1. $f(u,v)$ is always an non negative integer.
2. $C = \sum_{e=out(s)} c(e) \leq V(\text{max flow})$
3. Every iteration improves value of the flow by at least one

After observing these, the algorithm terminates after at most $C$ iterations.

The running time is $O(n + m)$, $n = |V|, m = |E|$

It is $O(m)$ if every node is reachable from the source.

The running time of FF is $\Theta(mC)$ which is psuedo-polynomial.

We can improve this by picking augmenting paths cleverly.

1. Pick "widest" path (maximum $b$) This results in $O(m\log C)$ iterations, which is polynomial. This results in $O(m^2\log C)$ for running time
2. Pick the path with the fewest edges. This results in $O(mn)$ iterations, which results in an $O(m^2 n)$ time algorithm.

### Lecture: Monday, November 18, 2019

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