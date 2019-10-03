# CSCC46

## Lecture Notes

### LEC 1: Monday, September 9, 2019

Basically Networks.

How can we analyze networks?

- Node Classification: We can predict the type of a given node
- Link Prediction: We can predict whether two nodes are linked
- Community Detection: We can identify densely linked clusters of nodes
- Social Influence: We can predict common pathways
- Network Similarity: We can measure similarity between nodes and networks

A Network is a **Graph**; a collection of **Nodes** (set $N$) that are connected by **Edges** (set $E$). $G(N,E)$

**Networks** often refer to real systems, while **Graphs** are methematical representation of a network.

**Directed Networks** have directed edges

**Undirected Networks** have symmetrical edges

**Connected Components (undirected):**

- Any two vertices can be joined by a path
- No superset with the same property

A **disconnected graph** is made up of two or more connected components.

A **Bridge edge** is an edge that if we erase, then the graph becomes disconnected

An **Articulation point** is a point that if we erase, then the graph becomes disconnected

**Strongly connected directed graphs** have a path from each node to every other node.

**Weakly connected directed graphs** is connected if we disregard the edge directions

What does the Web look like? The web looks like a directed graph

$In(v) = \{ w | w \text{ can reach } v \}$

$Out(v) = \{ v | w \text{ can reach } v \}$

**Strongly Connected** can also be defined as a graph $G=(V,E)$ where $\forall A \in V, In(A) = Out(A)$

**Directed Acylic Graph (DAG)** is a graph that has no cycles

- i.e. $\forall A,B \in V, \text{ If } B \in In(A) \text{ Then } A \not\in In(B)$

**Strongly Connected Component (SCC)** is a set of nodes $S$ such that:

- every pair of nodes $S$ can reach each other
- There is no larger set containing $S$ with this property

**Fact:** Every Directed Graph is a DAG on its SCCs (so if we turn SCCs into Nodes)

**Claim:** SCCs partitions nodes of $G$. Meaning that each node is a member of exactly 1 SCC

**Proof of Claim:** By Contradiction:

- Suppose there exists there exists a node $v$ which is a member of two SCCs $S$ and $S'$, but then $S \cup S'$ is one large SCC. Contradiction!

**Claim:** $G'$ (graph of SCCs) is a DAG ($G'$ has no cycles)

**Proof of Claim:** By Contradiction:

Assume $G'$ is not a DAG, then $G'$ is a directed cycle. Now all nodes on the cycle  are mutually reachable and all are part of the same SCC. But then $G'$ is not a graph of connections between SCCs. Contradiction.

**Fact:** $Out(A) \cap In(A)$ is a Strongly Connected Component

##### Structure of The Web

Bow-tie.

Millions of Nodes going into a large SCC

A large SCC

Millions of nodes coming out of the SCC

Tendrills sticking out of the IN and OUT sections

Tubes connecting IN and OUT sections, bypassing the SCC

### LEC 2: Monday, September 16, 2019

How do we represent graphs?

- Edge lists, which are pairs $(x,y)$ where $x$ is the origin and $y$ is the destination (for directed graphs)
  - example: $[(1,2), (2,3)]$
- (We are assuming that there are no isiolated nodes btw)
- Adjaceny Lists, which are dictionaries which map origins to a list of destinations
  - example: ${1: [2,4], 2: [1,4], 3: [4]}$
- Adjacency Matrix, where $A_{ij} = 1$ means that there is a link from node $i$ to node $j$ and $A_{ij} = 0$ if otherwise
- Undirected and Directed graphs
  - Undirected Graphs have Undirected Links
  - Directed Graphs have Directed Links
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
  - $k_j$ Node degree: the number of edges adjacent to node $j$
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

### LEC 3: Monday, September 23, 2019

#### Strength of Weak Ties

**Networks: Flow of Information**

- How does information flow through networks?
  - What role do links (short vs long) and nodes play?
- How people find out new jobs?

**Granovetter's Answer**

- Structural: Friendships span different parts of the network
- Interpersonal: Friendship between two people vary in strength, you can be close or not close to someone.

Note: Friendships can span two communities and friendships can be within communities.

**Structural Force: Triadic Close**

Triangles are more likely to be closed in social networks (you are more likely to make friends with someone if you have mutual friends with them).

Triadic Closures result in a High Clustering coefficient.

**Reasons:**

- If $B$ and $C$ have a friend $A$ in common, then
  - $B$ is more likely to meet $C$
  - $B$ and $C$ trust each other

**Granovetter's Explanation**

- Granovetter makes a connection between social and structural role on an edge
- First Pont: Structure
- Second Point: Information

**Network Vocabulary**

- Span (bridge): The span of an edge is the distance of the edge endpoints if the edge is deleted
- Bridge edge: If removed, it disconnects the graph
  - span of a bridge edge = $\infty$
- Local Bridge: Edge of span > 2 (any edge that doesnt close a triangle)
  - Idea: Local bridges with long span are like real bridges

**Granovetter's Explanation**

- Model: Two types of edges: Strong (friend), Weak (acquaintance)
- Model: Strong Triadic Closure Property: Two strong ties imply a third edge
- Fact: If strong triadic closure is satisfied, then local birdges are weak ties.

**Claim:** If node $A$ satisfies the Strong Triadic Closure and has two strong ties, then any local bridge adjacent to A must be a weak tie.

Proof: By Contradiction

- Assume A satisfies the strong triadic closure and has two strong ties
- Let $A-B$ be a local bedge, assume it is a strong tie
- Then $B-C$ must exist because of strong triadic closure
- But then $A-B$ is no longer a local birdge, because its span is 2.

Granovetter's theory leads to strong ties being in clusters and weak ties bridging the different clusters.

Weak ties have access to different parts of the network. Access to other sources and other kinds of information. Strong ties have redundant information.

#### Tie Strength in Real Data

For many years, this theory was not tested, so it is legit? Yes.

#### Neighbourhood Overlap

- Edge Overlap: as the number of shared neighbours divided by the union of neighbours $O_{ij} = \frac{N(i) \cap N(j)}{N(i) \cup N(j)}$
  - $O_ij = 0$ implies a local bridge

#### Link Removal by Strength

- An important, recurring concept in network analysis is network robustness: how quickly does the graph become disconnected as you remove links?
- The faster the netwrok falls apart, the more prone to failure it is
- Test importange of edges by changing the order in which you remove them
- In the mobile call graph, we will test the importance of strong/weak edges, as well as high/low overlap edges, by employing this strategy?
  - **low to high** disconnects the network sooner
  - **high to low** does the opposite
  - This is more evident if we do this based off overlap

#### Network Communities

- Granovetter's stength of weak ties theory suggests that networks are compoased of tightly connected sets of nodes
- Network communities: sets of nodes with lots of connections inside a few to outside (the rest of the network)

#### Social Network Data

Zachary's Karate Club Network: Observe social ties and rivalries in a university karate club

- During his observation, conflicts led to the group to split
- Split could be explained by a minumum cut in the network.

#### Graph Partitioning

Two general approaches:

1. Start with every node in the same cluster and break apart at "weak links" ("divisive clustering")
2. Start with every node in its own community and join communities that are close together "agglomerative clustering"

**Girvan-Newman Algorithm**

- Divisive hierarchical clustering based on the notion of edge betweenness (number of shortests paths passing through an edge)
- Girvan-Newman Algo
  - Repeat until no edges are left:
    - (Re)calculate betweenness of every edge
    - Remove edges with highest betweenness (if ties, remove all edges tied for highest)
    - Connected components are communities
- Gives a hierarchical decomposition of the network

**Dendrogram**

- Graphical depiction of the hierarchical clustering splits done at every step

Note: How do we compute betweenness? Computing every pair is commutationally challenging.

- If we want to compute betweenness of paths starting at node A, we do a BFS starting from A.
- Count the number of shortests paths from A to all other nodes in the graph