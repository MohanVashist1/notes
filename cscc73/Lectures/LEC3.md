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