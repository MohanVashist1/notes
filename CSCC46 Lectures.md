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