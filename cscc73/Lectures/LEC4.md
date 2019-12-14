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