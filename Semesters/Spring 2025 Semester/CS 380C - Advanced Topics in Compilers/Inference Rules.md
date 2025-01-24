
## Role of inference rules

Given [[Context-Free Grammars|grammar]], we need to compute certain sets that will be used by the parser. These sets are usually specified recursively (e.g. if $A$ is a member of the set, then $B$ is also a member of the set).

From these rules, it is easy to write down code.

Heavily reliant on the definition of [[Rules of Inference]] and [[Well-Formed Formulae]].

## Parsing SLL(1) Grammars

Java uses this.

Compute relations `NULLABLE`, `FIRST`, and `FOLLOW`. 

- `NULLABLE`$\in N$ 
	- set of [[Context-Free Grammars#^56b2d0|non-terminals]] that can be rewritten into an empty string
- `FIRST(A)`$\in TU{\epsilon}$
	- if $A$ can be rewritten to a string starting with [[Context-Free Grammars#^f9b1d7|terminal]] $T$, then $T$ is in `FIRST(A)`
- `FOLLOW(A)`$\in T$
	- set of terminals that can follow A in a sentential form
	- $t\in$`FOLLOW(A)` if we can derive a string $At$.

These relations are defined for any context-free grammar, but if the grammar is SLL(1), they can be used to implement a recursive-descent parser.

### Nullable

$\epsilon$ production
- A production whose righthand side is the empty string $\epsilon$

Nullable non-terminal
- Non-terminal that can be rewritten to $\epsilon$

`NULLABLE`: Set of nullable non-terminals
- If there is a production $A\to \epsilon$, then $A\in$`NULLABLE`
- If there is a production $A\to Y_{1}\dots Y_{n}$ and $Y_{i}\in$`NULLABLE` for all $Y$, then $A\in$`NULLABLE`

#### Inference Rules for `NULLABLE`

`NULLABLE`$\in N$

$$
((A\to \epsilon)\in P)\implies (A\in \text{NULLABLE})
$$

$$
(((A\to Y_{1}\dots Y_{n})\in P) \cap (Y_{1}\dots Y_{n}\in \text{NULLABLE})) \implies(A\in \text{NULLABLE})
$$

Given a proposal that $X\in N$, we can check if the proposal is consistent with inference rules. We want the smallest set that satisfies **all** the inference rules.

##### Example

Given the grammar:
$$
\begin{align}
S\to A$ \\
A\to BC|x \\
B\to t|\epsilon \\
C\to v|\epsilon \\
\end{align}
$$
- {} is **not** consistent
- {A} is **not** consistent
- {A,B,C} **is** consistent
- {S,A,B,C} **is** consistent

#### Computing NULLABLE

Initialize `NULLABLE` to `{}`

We do a round-based computation
- In each round, visit every production and see if you can add more elements to `NULLABLE`. Terminate when `NULLABLE` does not change in some round.

### FIRST

