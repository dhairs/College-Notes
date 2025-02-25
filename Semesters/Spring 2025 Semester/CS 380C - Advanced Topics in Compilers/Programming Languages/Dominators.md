
## What is a Dominator

In a [[Control Flow Graphs|control flow graph]] $G$, node $a$ is said to dominate node $b$ if every path from `START` to $b$ contains $a$.

### Dominance Properties

- **Reflexive**: $a\text{ dom } a$
- **Anti-symmetric**: $a\text{ dom } b$ and $b\text{ dom } a\implies a=b$
- **Transitive**: $a\text{ dom } b\cap b\text{ dom }c \implies a\text{ dom } c$
- **Tree-structured**:
	- $a\text{ dom } c \cap b\text{ dom }c\implies a\text{ dom } b \;\cup\;b\text{ dom }a$
	- Intuitively, this means that dominators of a node are themselves ordered by dominance

### Dominance Relation: relation on nodes

We write $a\text{ dom }b$ if $a$ dominates $b$.

#### Computing Dominance Relation

The domain of this relation is the [[Power Set|power set]] of nodes in the CFG.

There is a [[Dataflow Analysis|dataflow problem]]. If we have a node with multiple inputs, how do we get dataflow information.

$\text{Dom}(N)=\{N\}\cup M \in\text{pred}(N)\cap\text{Dom}(M)$.

### Example CFG

```mermaid
graph TD
    A[START] --> B(a)
    B --> C(b)
    C --> D(c)
    D --> E{d}
    D --> F{e}
    E --> G(f)
    F --> G
    G --> C
    B --> D
    G --> H(g)
    H --> I[END]
    A --> I
```


|       | Start | A   | B   | C   | D   | E   | F   | G   | END |
| ----- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
| Start |       |     |     |     |     |     |     |     |     |
| A     |       |     |     |     |     |     |     |     |     |
| B     |       |     |     |     |     |     |     |     |     |
| C     |       |     |     |     |     |     |     |     |     |
| D     |       |     |     |     |     |     |     |     |     |
| E     |       |     |     |     |     |     |     |     |     |
| F     |       |     |     |     |     |     |     |     |     |
| G     |       |     |     |     |     |     |     |     |     |
| E     |       |     |     |     |     |     |     |     |     |

### Building Dominator Tree Directly

Based on depth-first-search (DFS) of graph.

$O(E*\alpha(E))$ where $E$ is the number of edges in a CFG.

This runs in essentially linear time (the inverse Ackermann function $\alpha$ grows incredibly slowly).

There is a linear time algorithm, but its a lot more complex and not efficient to implement for extremely large graphs.

## Immediate Dominators

The immediate dominator of a node $n$ is the parent of the node, if it exists.
- Denoted as $\text{idom}(n)$
- There is no $\text{idom}$ for `START`

As a result, all dominators of $n$ other than $n$ itself dominate $\text{idom}(b)$.