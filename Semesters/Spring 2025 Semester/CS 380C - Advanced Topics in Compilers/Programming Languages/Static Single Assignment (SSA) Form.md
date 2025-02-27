## Definition

Static Single Assignment (SSA) is an intermediate representation of a program in which every use of a variable is reached by **exactly** one definition.

Most programs do not satisfy this condition.

It requires inserting dummy assignments called $\Phi$-functions (**Phi functions**) at merge points in the [[Control Flow Graphs|CFG]] to "merge" multiple definitions

Simple algorithm: insert $\Phi$-functions for all variables at all merge points in the CFG and rename each real and dummy assignment of a variable uniquely.


## Minimal SSA Form

In some cases, a dummy $\Phi$-function is unneeded 
## Computing Minimal SSA

We need to compute the merge relation $M$: $V\to P(V)$

If node $N$ contains an assignment to a variable $x$, then node $Z$ is in $M(N)$ if:
- There is a non-null path $P_{1}:=N\to ^{+}Z$
	- The value computed at $X$ reaches $Z$
- There is a non-null path $P_{2}:=\text{START}\to ^+Z$
- $P_{1}$ and $P_{2}$ are disjoint except for $Z$

If $S \subseteq V$ where there are assignments to variable $x$, then place $\Phi$-functions for $x$ in nodes $\bigcup_{N\in S}M(N)$.