# CSCC73

## Lecture Notes

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
  - $f := $ augment$(f,p)$
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

So we have proved that this algorithm terminates and know it's complexity.

Now we must prove Correctness.

<u>Correctness of FF</u>

<u>Lemma 2:</u> $\forall$ flow $f$, $\forall$ cut $(S,T)$ of $F$

Note that:

$out(S) = \bigcup_{u \in S} out(u)$

$in(S) = \bigcup_{u \in S} in(u)$

So for lemma 2, $V(f) = \sum_{e \in out(S)\cup in(T)} f(e) - \sum_{e\in out(T) \cup in(S)} f(e)$

<u>Collorary 3:</u> $\forall$ flow $f$, $\forall$ cut $(S,T)$, $V(f) \leq c(S,T)$

Proof: $V(f) = \sum_{e \in out(S)\cup in(T)} f(e) - \sum_{e\in out(T) \cup in(S)} f(e) \leq \sum_{e \in out(S)\cup in(T)} f(e) = c(S,T)$

<u>Collorary 4:</u> $\forall$ flow $f, \forall$ cut $(S,T)$

if $V(f) = c(S,T)$ then $f$ is a max flow and $(S,T)$ is a min cut

Proof: 

Let $f^*$ be the flow computed by FF

$S^* :=$ set of nodes reachable from $s$ in $G_{f^*}$

$T^* = V - S^*, s\in S^*, t \not\in S^*$[by termination condition]

And this implies that $t \in T^*$

Which implies that $(S^*, T^*)$ is a cut

We will show that:

(a) $\forall e \in out(S^*) \cap in(T^*), f^*(e) = c(e)$

(b)$\forall e \in out(T^*) \cap in(S^*), f^*(e) = 0$

We are done after we prove these, as

$V(f^*) = \sum_{e \in out(S)\cup in(T)} f^*(e) - \sum_{e\in out(T) \cup in(S)} f^*(e) = c(S^*, T^*)$

By Cor 4, $f^*$ is max, $(S^*,T^*)$ is min

Proof of (a), we want to show that an edge $e=(u,v), u \in S^*, v \in T^*$ is full. Assume for contradiction that $f^*(u,v) < c(u,v)$. This implies that $G_{f^*}$ contains a forward edge $(u,v)$, $v$ is reachable from $s$ in $G_{f^*}$ [because $u$ is, since $u\in S^*$]. Therefore $v \in S^*,$ which is a contradiction.

Proof of (b). Assume for contradiction that, $f^* (u',v') > 0$, then $G_{f^*}$ contains a backward edge $(v',u')$. This implies that $u'$ is reachable from $s$ in $G_{f^*}$ because $v'$ is, since $v' \in S^*$. Therfore,  $u' \in S$, which is a contradiction.

<u>Algo to Find Minimum Cut</u>

- Run FF to find a max flow $f$
- compute the residual graph $G_f$
- $S :=$ set of nodes reachable from $s$ in $G_f$
- $T := V -S$
- return $(S, T)$

<u>Max Flow Min Cut Theorem</u>

In every flow network, the value of the max flow = capacity of minimum cut

The Running time of the Minimum Cut Algorithm is Dominated by the Ford Fulkerson Algorithm.

<u>Integrality Theorem</u>: If all capacities are integers, there exists a max flow where every edge has an integer amount of traffic.

Proof of Lemma 2: $V(f) = \sum_{e\in out(S) \cap in(T)} f(e) - \sum_{e\in out(T) \cap in(S)} f(e)$

$V(f) = \sum_{u \in S} [\sum_{e \in out(u)} f(e) - \sum_{e \in in(u)} f(e)] $ 

