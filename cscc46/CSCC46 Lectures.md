# CSCC46

## Lecture Notes

### LEC 1: Monday, September 9, 2019

Basically Networks.

How can we analyze networks?

- We can predict the type of a given node
- We can predict whether two nodes are linked
- We can identify densely linked clusters of nodes
- We can predict common pathways

A Network is a **Graph**; a collection of **Nodes** that are connected by **Edges**.

**Networks** often refer to real systems, while **Graphs** are methematical representation of a network.

**Connected Components (undirected):**

- Any two vertices can be joined by a path
- No superset with the same property

A **disconnected graph** is made up of two or more connected components.

A **Bridge edge** is an edge that if we erase, then the graph becomes disconnected

An **Articulation point** is a point that if we erase, then the graph becomes disconnected

**Strongly connected directed graphs** have a path from each node to every other node.

**Weakly connected directed graphs** is connected if we disregard the edge directions

$In(v) = \{ w | w \text{ can reach } v \}$

$Out(v) = \{ v | w \text{ can reach } v \}$

**Strongly Connected** can also be defined as a graph $G=(V,E)$ where $\forall A \in V, In(A) = Out(A)$

**Directed Acylic Graph (DAG)** is a graph that has no cycles

- i.e. $\forall A,B \in V, \text{ If } B \in In(A) \text{ Then } A \not\in In(B)$

**Strongly Connected Component (SCC)** is a set of nodes $S$ such that:

- every pair of nodes $S$ can reach each other
- There is no larger set containing $S$ with this property

Every Directed Graph is a DAG on its SCCs (so if we turn SCCs into Nodes)

**Claim:** SCCs partitions nodes of $G$. Meaning that each node is a member of exactly 1 SCC

**Proof of Claim:** By Contradiction:

- Suppose there exists

**Claim:** $G'$ (graph of SCCs) is a DAG

**Proof of Claim:** By Contradiction:

Assume $G'$ is not a DAG, then $G'$ is a directed cycle

### LEC 2: Monday, September 16, 2019

How do we represent graphs?

- Edge lists, which are pairs $(x,y)$ where $x$ is the origin and $y$ is the destination (for directed graphs)
  - example: $[(1,2), (2,3)]$
- (We are assuming that there are no isiolated nodes btw)
- Adjaceny Lists, which are dictionaries which map origins to a list of destinations
  - example: ${1: [2,4], 2: [1,4], 3: [4]}$
- Adjacency Matrix, where $A_{ij} = 1$ means that there is a link from node $i$ to node $j$ and $A_{ij} = 0$ if otherwise
- Undirected and Directed graphs
- Unweighted and weighted graphs
  - $\bar k$ (or $\langle k \rangle$) is the average degree of all nodes in the graph
  - $E$ is the number of edges in the graph
- Graphs with self-edges
- Multi-graphs (graphs with multiple edges between the same pair of nodes $A,B$)
- Bipartite graph (nodes can be divided into two disjoint sets and all edges go from one set to another)
  - There is also the "folded version" in which $A,B$ in one set are linked if they connect to the same node in the other set.

However, real-world networks are usually sparse, so Adjaceny matrix representations will be filled with 0s.

<u>Examples: Network Representations</u>

WWW - Directed Self-edge Multi-graph

Facebook - Undirected Weighted Graph

How do we measure properties of a graph representation of a network?

We'll focus on **connectivity** and **distance**

<u>Connectivity:</u>

- Undirected
  - $k_j$ Node degree: the number od edges adjacent to node $j$
  - Average degree: $\bar k = \langle k \rangle = \frac{1}{N} \sum^N_{i=1} k_i = \frac{2E}{N}$
- Directed
  - Source: Node with $k^{in} = 0$
  - Sink: Node with $k^{out} = 0$
  - Degree of a node is indegree + outdegree
  - outdegree: outgoing nodes
  - indegree: ingoing nodes
  - $\bar k^{in} = \bar k^{out}$
- Degree distribution $P(k)$: Probability that a randomly chosen node has degree $k$
- $N_k = $ number of nodes with degree k
- Normalized histogram: $P(k) = N_k / N$
- Local Clustering
  - Are nodes "clustered" in the graph?
  - Clustering Coefficient, what's the probability that a random pair of your friends are connected?
    - $C_i \in [0,1]$
    - $C_i = \frac{e_i}{{k_i \choose 2}} = \frac{e_i}{k_i (k_i-1) (1/2)} = \frac{2e_i}{k_i (k_i-1)}$ 
      - $e_i$ is the number of edges between the neighbours of node $i$
      - $k_i$ is the degree of node $i$
    - Average Clustering Coefficient = $\frac{1}{N} \sum^N_{i=1} C_i$
- Paths in a Graph
  - a **Path** is a sequence of nodes in which each node is linked to the next one
  - A path can intersect itself and pass thrugh multiple edges
  - In a directed graph, they can only follow the edge directions
  - Numbers of Paths
    - length $h = 1$: If there is a link between $u,v$, then $A_{uv} = 1$ else $A_{uv} = 0$
    - length $h=2:$ If there is a path of length 2 between $u,v$ then $A_{uk}A_{kv} = 1$ else 0, we can also get it by multiplying the matrix with itself as such
    - length $h=k$: Multiply the Matrix by itself $k$ times.
- Distance:
  - Distance (shortest path): the distance between a pair of nodes is defined as the number of edges along the shortest path connecting the nodes
  - In directed graphs, paths need to follow the direction of the arrows, so distance may not be symmetric.
  - Diameter: The maximum shortest path distance between any pair of nodes in a graph
  - Average path length: The average path length for a strongly connected component.

We don't really know how to tell if a graph's properties are "normal". So we need a model to compare

##### Simplest Model of Graphs

Erdös-Renyi Random Graphs:

$G_{n,p}$: undirected graph on $n$ nodes and each edge appears with probability $p$ 

The graph is the result of a random process.

**How likely is a graph with $E$ edges?**

$P(E):$ the propbability that a given $G_{np}$ generates a graph with exactly $E$ edges

$P(E) = {E_{max} \choose E} p^E (1-p^{E})$

**What is the expected degree of a node?**

Let $X_v$ be a random variable mesuring the degree of node $v$

We want to know $E[X_v] = \sum^{n-1}_{j=0} j P(X_v = j) = (n-1)p$

