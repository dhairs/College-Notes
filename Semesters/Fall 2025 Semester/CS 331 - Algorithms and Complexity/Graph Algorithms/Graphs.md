## Exploring an Undirected Graph from a Specified Vertex

Assume we're given a graph $G=(V,E)$ in adjacency list format. Let $s$ be a specified source vertex. We want to systematically visit all of the vertices and edges of the connected component of $G$ that contains $s$.

This is easier in a tree because we can just move between left and right and guarantee you don't see the same node twice.

In graph **breadth-first search (BFS)**, we explore by distance from the source node. If an edge allows us to discover a new node at the next level, we call it a **tree edge**.

We can use a first-in first-out (FIFO) queue to find what we need to discover.

In graph **depth-first search (DFS)**, we start at $s$ and look for a new node. Once we find new node $A$, we recursively add a search starting at $A$ to the call stack and mark the edge as a tree edge. We keep searching until we reach a base case (no more new tree edges). Then, we pop out of the stack and continue the search until we reach a base case at each call in the call stack. 

If we run BFS/DFS from a single source vertex $s$, we only explore the connected component of $s$. To ensure that we explore the entire graph, we introduce an "outer loop" over all vertices in $V$. When the outer loop reaches a vertex, we check if we have visited it already. If we've visited it already, don't do anything, otherwise do a DFS/BFS from that vertex.

## Spanning Tree

The spanning tree of an undirected graph is simply a **connected, acyclic subgraph**.

The spanning tree of $G=(V,E)$ where $G$ is undirected, can only exist if $G$ is connected.  If it is not connected, we can have a **spanning forest**.

If we do a BFS or DFS and mark edges that allow us to find a new node as tree edges, once we're done exploring the graph, the tree edges form a spanning tree.

## Recognizing Bipartite Graphs

An undirected graph $G=(V,E)$ is bipartite if the vertex set $V$ can be partitioned into two sets $V'$ and $V''$ such that every edge in $E$ has exactly one endpoint in $V'$ (and thus also one in $V''$).

It's easy to prove that $G$ is bipartite if and only if $G$ does not contain and odd-length cycle.

Alternatively, $G$ is bipartite if and only if it is [[Coloring of a Graph|2-colorable]].


> [!faq] How can we use BFS/DFS to determine whether $G$ is 2 colorable in linear time?
> We can assign a color to each edge as we explore it. Whenever we label an edge as non-tree, we need to make sure that the two vertices of the edge violate the coloring of the graph. If it does, then the graph is not two-colorable.

## Single Source Shortest Paths (SSSP)

Let $G=(V,E)$ be an undirected graph with a specified vertex $s$. If we run BFS from $s$, we get a spanning tree $T$ of the connected component of $G$ that contains $s$, we'll call it $G'=(V',E')$.

## BFS/DFS in a Digraph $G=(V,E)$

The procedures for BFS/DFS in undirected graphs generalize in a natural way to digraphs. In the directed case, each edge is encountered exactly once. The 

## Strongly Connected Components (SCC)

Let $G=(V,E)$ be a given digraph. We say that vertices $u$ and $v$ belong to the same **strongly connected component (SCC)** of $G$ if $v$ is reachable (via a directed path) from $u$ and $u$ is reachable from $v$.

Let the binary relation $R$ denote the set of pairs $(u,v)$ in $V\times V$ such that $u$ and $v$ belong to the same SCC. The relation $R$ is reflexive, symmetric, and transitive. It is an equivalence relation.

$R$ thus partitions $V$ into equivalence classes, each of which corresponds to the vertex set of an SCC of $G$.

### Identifying the SCC of a Given Vertex

Let $G=(V,E)$ be a given digraph and let $s$ be a specified vertex in $V$. 


> [!FAQ] How can we use BFS/DFS to determine the SCC of $s$ in linear time?
> Contents

## Applications of Directed DFS


## Directed Cycle Detection in Digraphs

Recall that an undirected graph $G$ contains a cycle if and only if any DFS of $G$ yields a non-tree edge.

For digraphs, we can say the following: A digraph $G$ contains a directed cycle if and only if any DFS of $G$ yields a back edge.
