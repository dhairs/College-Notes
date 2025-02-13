## Fixpoint Equations

Fixpoint equations are elementary equations. They are represented in the form $x=f(x)$.

## Domain

A domain is a finite partially-ordered set with a least element. The domain is a set with the order relation $\leq$.

## Monotonic Functions

The function $f: D\to D$ where $D$ is a domain is monotonic if:
- $x\leq y\to f(x)\leq f(y)$

The function must map elements that are less than or equal to each other to elements that are also less than or equal to each other.

A **different** property that is often confused with monotonicity is **extensivity**, which says that $x\leq f(x)$.

### Intuition

Think of $f$ as an electrical circuit mapping input to output. $f$ is monotonic if increasing the input voltage causes the output voltage to increase or stay the same. $f$ is extensive if the output voltage is greater than or equal to the input voltage.

## Fixpoint of the function of a domain

Suppose $f:D\to D$, a value $x$ is a **fixpoint** of $f$ if $f(x)=x$. $f$ maps $x$ to itself.

### Example with D being a powerset of {a,b,c}

Identity function: $x\to x$
- Every point in the domain is a fixpoint of this function

$x\to x\cup \{a\}$
- {a}, {a,b}, {a,c}, {a,b,c} are all fixpoints

$x\to \{a\}-x$
- no fixpoints

## Fixpoint Theorem with Multiple Functions

If $D$ is a domain and $f,g:D\times D\to D$ are monotonic, the following system of simultaneous equations has a least solution computed in the obvious way:
- $x=f(x,y)$
- $y=g(x,y)$

You can generalize this to more than two equations and to the case when $D$ has a greatest element $T$.

### Example with Multiple Functions

$$
\begin{align} 
\begin{pmatrix}
x_{n+1} \\
y_{n+1}
\end{pmatrix} = \begin{pmatrix}
f(x_{n},y_{n}) \\
g(x_{n}, y_{n})
\end{pmatrix}
\\
\begin{pmatrix}
\bot \\
\bot
\end{pmatrix},\begin{pmatrix}
f(\bot,\bot) \\
g(\bot,\bot)
\end{pmatrix}, \dots
\end{align}
$$
## Power-Set Domains ($\cap \text{ and } \cup$)

Consider a [[Power Set|power set]] domain
- Set union and intersection are monotonic functions
- So we can use them in systems of fixpoint equations

> [!faq]- Things to think about
> If a system of fixpoint equations has multiple equations for an unknown, is the system still guaranteed to have a solution?
> Ex: consider the system $x=f(x)$ and $x=g(x)$

### Example of Power-Set Domain

$f(x,y) = \{a\}$

Equations: 
$$
\begin{align}
x=f(x,y) \\
y=x\cup y
\end{align}
$$

## Join and Meet

If $(D,\leq)$ is a [[Partially Ordered Set|poset]] and $e_{1},e_{2} \in D,\ell\in D$ is a lower bound of $\{e_{1},e_{2}\}$ if $\ell\leq e_{1} \text{ and } \ell\leq e_{2}$. 

This is an easy generalization to lower bound of a set $S$ of elements from $D$.

In general, a set $S$ may have many lower bounds.

**Greatest lower bound (glb)** of $S$: greatest element of $D$ that is a lower bound of $S$:
- Caveat: glb may not always exist

If for every pair of elements $x,y\in D$ glb({x,y}) exists, we can define a function called **meet**($\wedge:D \times D\to D$)
- $x\wedge y=glb(\{x,y\})$
- Meet is idempotent ($\text{meet}(x) = x$), commutative, and associative

**Meet semilattice**: a partially ordered set inw hich every pair of elements has a glb

Analogous notions: upper bounds, least upper bounds, join ($\vee$)

**Join semilattice**: analogous notion

**Lattice**: both a meet and join semilattice