## Definition

Static Single Assignment (SSA) is an intermediate representation of a program in which every use of a variable is reached by **exactly** one definition.

Most programs do not satisfy this condition.

It requires inserting dummy assignments called $\Phi$-functions (**Phi functions**) at merge points in the [[Control Flow Graphs|CFG]] to "merge" multiple definitions

Simple algorithm: insert $\Phi$-functions for all variables at all merge points in the CFG and rename each real and dummy assignment of a variable uniquely.

## Minimal SSA Form

In some cases, a dummy $\Phi$-function is unneeded because there is no assignment between graph nodes. Minimal SSA form removes unnecessary dummy assignments. 

## Computing Minimal SSA

We need to compute the merge relation $M$: $V\to P(V)$

If node $N$ contains an assignment to a variable $x$, then node $Z$ is in $M(N)$ if:
- There is a non-null path $P_{1}:=N\to ^{+}Z$
	- The value computed at $X$ reaches $Z$
- There is a non-null path $P_{2}:=\text{START}\to ^+Z$
- $P_{1}$ and $P_{2}$ are disjoint except for $Z$

If $S \subseteq V$ where there are assignments to variable $x$, then place $\Phi$-functions for $x$ in nodes $\bigcup_{N\in S}M(N)$.

### Computing Merge($v$)

If $u\in \text{Merge}(w)$, $w$ does not strictly [[Dominators#What is a Dominator|dominate]] $u$
- Proof: there is a path from `START` to $v$ that does not contain $w$

Conversely, if $w$ dominates $u$, $u \notin \text{Merge}(w)$.

The idea is to compute nodes on the **dominance frontier** of $w$. $w$ does not strictly dominate $u$ but dominates some CFG predecessor of $u$. We just iterate on this.

The dominance frontier is the same as computing the [[Control-Dependence]] in the reverse direction.

## Iterated Dominance Frontier

Irreflexive closure of dominance frontier relation. Related notion: iterated control dependence in reverse graph.

## Why is SSA Form Useful?

For many dataflow problems, SSA form enables sparse dataflow analysis that yields the same precision as bit-vector CFG-based dataflow analysis but is asymptotically faster since it permits the exploitation of sparsity. (ex. constant propagation)

### Constant Propagation

Understand the problem of [[Scalar Optimizations#Constant Propagation|Constant Propagation]] in terms of scalar optimizations.

Intuition: discovers that the false side of the conditional is dead and allows for dead-code elimination.

#### Def-use Chains Algorithm

- Compute reaching definitions
- Add def-use chains to CFG
- Cell for each definition and use, initialized to $\bot$
- Propagate lattice values from definitions to uses, using confluence operator to merge values from multiple definitions that reach a given use

The algorithm will not find all the constants found by CFG dataflow algorithm.

#### SSA Algorithm (used by LLVM)

- Cells for each def and use of SSA edges initialized to $\bot$
- Cells per edge and statement to mark liveness
- Propagate liveness along CFG edges to mark live edges
- Statement is live if any incoming edge is live
- Propagate constants along SSA edges from live statements
- At conditional, evaluate condition using propagated values to mark liveness on outgoing edges
- At $\Phi$ function, merge values only from live CFG edges using confluence operator
- Will find all constants found by CFG dataflow algorithm