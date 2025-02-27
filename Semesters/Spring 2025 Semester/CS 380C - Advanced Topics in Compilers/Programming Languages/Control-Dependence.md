## Idea

Intuitively, node $w$ is control-dependent on a node $u$ if $u$ determines whether $w$ is executed.

### Example of Basic Control Dependence


| ![[Control Dependence Example Basic.png]]                                      |
| -------------------------------------------------------------------------- |
| https://www.cs.utexas.edu/~pingali/CS380C/2025/lectures/ssa/Dominators.pdf |

In this case, we would say that S1 and S2 are control-dependent on e.

### Example of Self Control Dependence



| ![[Control Dependence Example Self.png]]                                   |
| -------------------------------------------------------------------------- |
| https://www.cs.utexas.edu/~pingali/CS380C/2025/lectures/ssa/Dominators.pdf |

In this case, we would say:
- S1 is control-dependent on e.
- e is control dependent on `START` and itself

### Example with Transitive Control Dependence


| ![[Control Dependence Example Transitive.png\|400]]                        |
| -------------------------------------------------------------------------- |
| https://www.cs.utexas.edu/~pingali/CS380C/2025/lectures/ssa/Dominators.pdf |

In this case, we would say:
- S1 and S3 are control-dependent on f
- They are transitively dependent on e, but e does not fully determine if S1 or S3 are executed, so S1 and S3 are **not** control-dependent on e
- However, we can say that f is control-dependent on e and S1 and S3 are transitively control-dependent on e

## Definition

For $w$ to be control-dependent on edge $u\to v$, $w$ must [[Dominators#Postdominators|postdominate]] $v$ for some CFG successor $v$ of $u$, $w$ can not be $u$, and $w$ can not $\text{pdom } u$.

Intuitively, if control flows from $u$ to $v$, it is guaranteed that $w$ will be executed. But from $u$ we can reach `END` without encountering $w$, so there is a decision being made at $u$ that determines whether or not $w$ is executed.

As a result, we can rewrite this to be:
- $w\text{ pdom }v$
- $w$ does not [[Dominators#Strict Postdominance|strictly postdominate]] $u$

### Example

Using the example from before: ![[Dominators#Example CFG]]

|          | A   | B   | C   | D   | E   | F   | G   |
| -------- | --- | --- | --- | --- | --- | --- | --- |
| Start->a | x   |     | x   |     |     | x   | x   |
| f->b     |     | x   | x   |     |     | x   |     |
| c->d     |     |     |     | x   |     |     |     |
| c->e     |     |     |     |     | x   |     |     |
| a->b     |     | x   |     |     |     |     |     |

An `x` marks control dependence. This is **not** transitive control dependence.

## Computing Control-Dependence Relation

Given a CFG $G$, a node $w$ is control-dependent on an edge $u\to v$ if:
- $w$ [[Dominators#Postdominators|postdominates]] $v$
- $w$ does not [[Dominators#Strict Postdominance|strictly postdominate]] $u$

Nodes control dependent on edge $u \to v$ are nodes on the path up from the postdominator tree from $v$ to $\text{ipdom}(u)$ excluding $\text{ipdom}(u)$
- Written as $[v,\text{ipdom}(u))$
	- Half-open interval in tree

Overlay each edge $u\to v$ on pdom tree and determine nodes in interval $[v,\text{ipdom}(u))$. The time and space complexity is $O(EV)$. 

However, in practice, we don't want the full relation and only make queries:
- cd($e$): what are the nodes control-dependent on an edge $e$
- conds($w$): what are the edges that is $w$ is control-dependent on
- cdequiv($w$): what nodes have the same control-dependences as node $w$

It is possible to create a simple data structure that takes $O(E)$ time and space to build and that answers these queries in time proportional to the output of the query.