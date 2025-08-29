
## Exploring an Undirected Graph from a Specified Vertex

Assume we're given a graph $G=(V,E)$ in adjacency list format. Let $s$ be a specified source vertex. We want to systematically visit all of the vertices and edges of the connected component of $G$ that contains $s$.

This is easier in a tree because we can just move between left and right and guarantee you don't see the same node twice.

In graph **breadth-first search (BFS)**, we explore by distance from the source node. If an edge allows us to discover a new node at the next level, we call it a **tree edge**.

We can use a first-in first-out (FIFO) queue to find what we need to discover.

In graph **depth-first search (DFS)**, 

## Spanning Tree

The spanning tree of an undirected graph is simply a **connected, acyclic subgraph**.

The spanning tree of $G=(V,E)$ where $G$ is undirected, can only exist if $G$ is connected.  If it is not connected, we can have a **spanning forest**.

If we do a BFS and mark edges that allow us to find a new node as tree edges, once we're done exploring the graph, the tree edges form a spanning tree.