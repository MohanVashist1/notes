# LEC 1 - NOT ADDED TO ANKI

**Networks**

refers to real systems Web, Social network, Metabolic network

**Graph**

mathematical representation of a network Web graph, Social graph

**Undirected Graphs**

Graphs with undirected links

**Directed Graphs**

Graphs with directed links

**Connected Component (undirected)**

- Any two vertices can be joined by a path
- No superset with the same property

**Bridge edge**

An edge that, if we erase it, the graph becomes disconnected

**Articulation Point**

A node that, if we erase it, the graph becomes disconnected

**Strongly connected directed graph**

has a path from each node to every other node and vice versa

**Weakly connected directed graph**

is connected if we disregard the edge directions

**How do we represent the web as a graph?**

Nodes = web pages, Edges = hyperlinks

**What kind of graph is the web?**

A directed graph

**What are the two types of directed graphs?**

- Strongly Connected
- Directed Acyclic Graph (DAG)

**Directed Acyclic Graph**

Has no cycles

**Strongly connected component (SCC)**

A set of nodes such that

- Every pair of nodes in the set can reach each other
- No larger set containing the set with this property

**Is every directed graph a DAG on its SCCs?**

Yes

**What is the structure of the web?**

The web is a bowtie structure

**What does the bowtie structure look like?**

- Giant component
- IN and OUT components
- Tendrils
- Disconnected Components

# LEC 2 - NOT ADDED TO ANKI

**How can we represent Graphs?**

- Edge List
- Adjacency List
- Adjacency Matrix

**Edge List**

List of edges between nodes

**Adjacency List**

Dictionary mapping Nodes to other nodes that they are connected to

**Adjaceny Matrix**

$A_{ij} = 1$ if there is a link from node $i$ to node $j$, $A_{ij} = 0$ otherwise

**Can Friendship on Facebook be represented by Undirected Graphs?**

Yes

**Can Phone calls be represented by Directed Graphs?**

Yes

**Unweighted Graphs**

Graphs with no edge weights

**Weighted Graphs**

Graphs with edge weights

**Graphs with self edges**

Graphs with edges that point from node a to node a

**Multigraph**

Graphs where there exists multiple edges between two nodes

**Bipartite graph**

Graph whose nodes can be divided into two disjoint sets of nodes $U$ and $V$ such that every link connects a node from $U$ to a node from $V$.

**Folded Bipartite Graph**

Only the set $U$ from the Bipartite graph, but nodes in $U$ have an edge between each other if they both have an edge between the same edge in $V$.

**Node Degree (Undirected)**

the number of edges adjacent to a specific node $(k_i)$

**Average Node Degree of an Undirected Graph**

$<k> = \bar{k} = \frac{1}{N}\sum^N_{i=1} k_i = \frac{2E}{N}$

**In-degree**

Degree of incoming edges of a node ($k^{in}$)

**Out-degree**

Degree of outgoing edges of a node ($k^{out}$)

**Node Degree (Directed)**

sum of all in-degrees and out-degrees

**Source**

Node with ($k^{in} = 0$)

**Sink**

Node with ($k^{out} = 0$)

**Degree Distribution**

Probability $P(k)$ that a randomly chosen node has degree $k$

**The number of edges between the neighbours of a node notation**

$e_i$ for a node $i$

**Clustering Coefficient**

$C_i = \frac{e_i}{k_i\choose 2} = \frac{2e_i}{k_i (k-1)}$

**Average clustering coefficient of a graph**

$C = \frac{1}{N} \sum^N_i C_i$

**Path**

A sequence of nodes in which each node is linked to the next one.

**Distance**

Defined as the number of edges along the shortest path connecting the nodes

**Is Distance symmetric in directed graphs?**

No

**Diameter**

The maximum (shortest path) distance between any pair of nodes in a graph

Average path length

for a connected graph component or a strongly connected component of a directed graph

$\bar{h} = \frac{1}{2E_{max}} \sum_{i, j | j \neq i} h_{ij}$

**Are most real-world networks sparse?**

Yes

**Erdös-Renyi Random Graphs**

An undirected graph $G_{n,p}$ on $n$ nodes and each edge $(u,v)$ appears iid with probability $p$

**iid**

independent and identically distributed

**How likely is a graph $G_{n,p}$ with $E$ edges?**

$P(E) = {E_{max}\choose E} p^E (1-p)^{E_{max} - E}$

where $E_{max} = \frac{n(n-1)}{2}$

**What is the expected degree of a node in a random graph?**

$E[X_v] = \sum^{n-1}_{u=1} E[X_{vu}] = (n-1) \cdot p$

**Is the degree distribution of $G_{np}$ Binomial?**

Yes

**What is the Clustering Coefficient of a random graph $G_{np}$?**

$C = p = \frac{\bar{k}}{n-1}$

**Are real networks like random graphs?**

No

**What are the problems with the random networks model?**

Clustering coefficient is too low

**What is the purpose of random graphs?**

- Reference model for anything interesting
- It helps us calculate many quantities that can then be compared to the real data

What are the Two perspectives on friendships?

- Structural
- Interpersonal

**Structural perspective on friendship**

Friendships span different parts of the network

**Interpersonal perspective on friendship**

Friendship between two people vary in strength, you can be close or not so close to someone

# LEC 3 - NOT ADDED TO ANKI

**Triadic Closure**

If two people have a friend in common, there is an increased likelihood that they will become friends themselves

**What are the reasons for triadic closure?**

If B and C have a friend A in common then

- B is more likely to meet C
- B and C trust each other
- A has incentive to bring B and C together

**Span**

The span of an edge is the distance of the edge endpoints if the edge is deleted

**Bridge edge**

If removed, it disconnects the graph

What is the Span of a bridge edge?

$\infty$

**Local Bridge**

Any edge of span $>2$

**What are the two types of edges in Granovetters' Explanation?**

- Strong Edge
- Weak Edge

**String Triadic Closure property**

Two strong ties imply a third edge

**What can we say about local bridges if the strong triadic closure is satisfied?**

Local bridges are weak ties

**What do weak ties have according to Granovetter?**

Weak ties have access to different parts of the network

**What do strong ties have according to Granovetter?**

Strong ties have redundant information

**$N(i)$ for a node $i$**

Set of neighbours of node $i$

**Edge Overlap**

The number of shared neighbours divided by the union of neighbours

$O_{ij} = \frac{N(i)\cap N(j)}{N(i)\cup N(j)}$

**Network Robustness**

A measure of how the graph becomes disconnected as you remove links

**How to test the importance of edges for Network Robustnesses?**

Test importance of edges by changing the order in which you remove them

**What kind of robustness does removing links by low/high strength have?**

Low, disconnects the network sooner

**What kind of robustness does removing links by low/high edge overlap have?**

Low disconnects the network much sooner compared to high

**What does Granovetter's strength of weak ties theory suggest?**

It suggests that networks are composed of tightly connected sets of nodes

**Network communities**

Sets of nodes with lots of connections inside and few to outside

**Zachary’s Karate club network**

- Observe social ties and rivalries in a university karate club 
- During his observation, conflicts led the group to split 
- Split could be explained by a minimum cut in the network

**What are the two general approaches to Graph Partitioning?**

- Divisive Clustering
- Agglomerative Clustering

**Divisive Clustering**

Swart with every node in the same cluster and break apart weak links

# LEC 4 - NOT ADDED TO ANKI

**Signed Networks**

Networks with edges labeled positive or negative

**Structural Balance**

Triangles where all edges are positive or only one is

**Structural Balance Intuition**

- Friend of my friend is my friend
- Enemy of my enemy is my friend
- Enemy of my friend is my enemy

**Balanced Graph**

A Complete graph is balanced if every connected triple of node has all 3 edges labeled + or exactly one edge labeled +

**Balance Theorem**

Balance implies global coalitions

**If all triangles are balanced then either _**

- Network only contains positive edges
- Network can be split into two factions where negative edges only point between the sets

**Weakly Balanced Graph**

A complete network is weakly balanced if there is no triangle with exactly 2 positive edges and 1 negative edge

**Characterization of Weakly Balanced Networks**

If a labeled complete graph is weakly balanced, then its nodes can be partitioned

**Is there a limit on how many global factions can exist in a network with a weak structural balance?**

No

**How do we check if incomplete graphs are balanced?**

- Local View
- Global View

**Local View of checking if Incomplete Graphs are balanced**

Fill in the missing edges to achieve balance

**Global View of checking if Incomplete Graphs are balanced**

If you can separate the graph into coalitions as before, call it balanced

**Are the Local View and Global View of checking if incomplete graphs are balanced the same?**

Yes

**Harary Theorem**

A Graph is balanced iff it contains no cycle with an odd number of negative edges

**Outline of Harary Theorem Proof**

- Constructing an Algorithm that either outputs a division into coalitions or a cycle with odd number of negative edges
- Algorithm can only fail of odd number of edges is discovered

How to check if a signed graph is balanced?

- Group positively connected components into super-nodes
- produce reduced graph on super-nodes
- use BFS to assign each super-node with a side
- grap is unbalanced if any two connected super-nodes are assigned the same side

**Embeddedness of link (A,B)**

Number of shared neighbours between A and B

**Embeddedness of ties**

Positive ties tend to be more embedded

**Homophily**

"Birds of the same feather flock together"

**Do connections form uniformly at random?**

No

**How do we measure homophily?**

Check if there are fewer connections between nodes across traits than you'd expect at random

**Homophily Test**

If the fraction of cross-gender edges is significantly less than random, then there is evidence of homophily

# LEC 5 - NOT ADDED TO ANKI

**Milgram's experiment**

- Picked ~300 people in Kansas
- Asked each person to try to get a letter to a particular person in Boston
- But they could only send the letter to someone they know on a first-name basis
- Each resulting chain took 6.2 steps on average

**The Bacon Number**

- Create a network of Hollywood actors
- Connect two actors if they co-appeared in a movie
- The number of steps to Kevin Bacon is the bacon number

**Criticism of Milgram experiment**

- Not that many samples
- Starting points and target were non-random
- 31 of 64 chains passed through 1 of 3 people (not all links/nodes are equal)

**Columbia Small-World Study**

- 18 diverse targets
- 24k first steps
- 65% dropout per step
- 1.5% of chains completed

**What was the problem with the Columbia Small-World Study?**

People stop participating

**Funneling effect**

Some target's friends are more likely to be the final step

**Effects of target's characteristics**

Structurally high-status target easier to find

**If assume each human is connected to 100 other people, in 5 steps we can each 10 billion people, what's wrong here?**

92% of new FB friends are to a friend-of-a-friend

**What are the basic properties of real social networks?**

Short paths

**How can we model short paths?**

Path lengths

**Rings**

Networks with high clustering and long paths

**Small-World Model's two components**

- Low-dimensional regular lattice
- Rewiring

**Low-dimensional regular lattice in the Small-World Model**

- Has high clustering coefficient
- Now introduce randomness ("shortcuts")
- (Ring can be used as a lattice)





