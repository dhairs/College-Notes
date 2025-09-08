## Minimum Spanning Tree Problem

We are given a connected, undirected graph $G=(V,E)$ where each edge $e$ in $E$ has an associated edge weight $w(e)$ which may be negative. A graph theoretic tree is a graph that is acyclic and connected.

A spanning tree $T$ of $G$ is a subgraph $G'=(V,E')$ of $G$ that is a tree. It is convenient to identify $T$ with its edge set. It is easy to prove that all spanning trees of $G$ have cardinality $|V|-1$.

The weight of a spanning tree $T$ is defined as $\sum_{e\in T} w(e)$.

A minimum spanning tree (MST) of $G$ is a spanning tree of $G$ of minimum weight.