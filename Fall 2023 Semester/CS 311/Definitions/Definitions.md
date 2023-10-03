## Definitions of Numbers
### Even Number

$Def^n$: An integer $n$ is said to be even if there exists an integer $k$ such that $n=2k$ ^ef410c

### Odd Number

$Def^n$: An integer $n$ is said to be odd if there exists an integer $k$ such that $n=2k+1$ ^dec16c

### Rational Number

$Def^n$: A real number $r$ is rational if there exists integers $p$ and $q$, where $q\neq0$, $r=\frac{p}{q}$ ^13fe65

### Irrational Number

$Def^n$: A real number $r$ is irrational if there exists integers $p$ and $q$, where $q\neq0$, $r=\frac{p}{q}$, and $p$ and $q$ have **no common factors**

### Absolute Value

^48abf7

$Def^n$: $|a|$ is the absolute value of $a$ and it equals $a$ when $a≥0$, and equals $-a$ when $a≤0$. ^4fb273

## Definitions of Sets
### Natural Numbers
$Def^n$: The set of natural numbers is defined to be 

$$\mathbb{N}=\{0,1,2,3,\ldots\}$$

Note that $0$ exists in this set. This is debated heavily, but for the purposes of this class, we assume it is a natural number.

### Integers
$Def^n$: The set of natural numbers is defined to be

$$Z=\{\ldots,-2,-1,0,1,2,\ldots\}$$

### Rationals
$Def^n$: The set of rational numbers is defined to be
$$Q=\{\frac{p}{q}|p\in{z}\wedge{q}\in{z}\wedge{q}\neq0\}$$

### Real
$\mathbb{R}$ 

### Empty Set/Null Set
Is simply $\{\}$ or $\varnothing$

### Singleton Set
A set with exactly one element.

$\{\varnothing\}$: singleton (we are saying that we have a Set with a null set within it)

### U: Universal
Refers to all the elements that are in the currently referenced scope.

### Ordered $n$-tuple
$Def^n$: $(a_1, a_2, \ldots, a_n)$ is an ordered collection of $n$ objects.

Note that there are **parentheses instead of curly brackets**. When this is the case, order *does* matter.

$(a_1, a_2, \ldots, a_n) = (b_1, b_2, \ldots, b_n)$ as long as

$$\begin{align}
a_1=b_1 \\
a_2=b_2 \\ 
\vdots \\
a_n=b_n
\end{align}$$
If $n=2$, then we have an **ordered pair.**

### Union
$$A\cup{B}$$
is defined as 

$$x\in A \vee x\in B$$

### Intersection
$$A\cap B$$

is defined as $$x\in A\wedge x\in B$$

### Difference
$$ A - B $$
is defined as 

$$x\in A \wedge \neg x\in B$$

### Complement

$$\overline{A}$$
is defined as

$$x\in U\wedge \neg x\in A$$
Complement of $B$ with respect to $A$ is the difference

### Set Identities


### Cardinality of Combined Sets (Principle of Inclusion-Exclusion)
$|A\cup B| = |A| + |B| - |A\cap B|$

$|A\cup B\cup C| = |A|+|B|+|C|-|A\cap B| - |B\cap C| - |C\cap A| + |A\cap B\cap C|$

$$|A\cup B\cup C\cup D| = |A|+|B|+|C|+|D|-|A\cap B| - |B\cap C| - |C\cap D| - |C\cap D| - |A\cap B| - |A\cap C| + |A\cap B\cap C| + |A\cap C\cap D|+|B\cap C\cap D|+|A\cap B\cap D|-|A\cap B\cap C\cap D|$$



$A_1\cup A_2$ 

$\bigcup\limits_{i=1}^{n}A_i$
