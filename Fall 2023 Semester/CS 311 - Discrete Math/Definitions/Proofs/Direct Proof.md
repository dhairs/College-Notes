## Definition

A direct proof of a conditional statement $p\to q$ is constructed by

- Assume $p$ is true
- Use rules of inferences, axioms, and logical (basic) equivalences to show that $q$ must follow

_Note: In some cases, you may want to use [[Direct Proof by Contraposition.md|direct proof by contraposition]]_

## Example 1: Give a direct proof of the theorem "If $n$ is an odd integer, then $n^2$ is odd."

$Def^n$: An integer $n$ is said to be even if there exists an integer $k$ such that $n=2k$

$Def^n$: An integer $n$ is said to be odd if there exists an integer $k$ such that $n=2k+1$

For direct proof, we will assume the hypothesis is true.

### Proof:

Assume $n$ is odd, then we have $n=2k+1$, for some integer $k$ (this is essentially a universal instantiation)

Squaring $n$, $n^2$, we get $n^2=2t+1$ where $t$ is an integer

$$
\begin{flalign}
n^2 \\
\equiv\, <\mathrm{substitution}> \\
(2k+1)^2 \\
\equiv\, <\mathrm{algebra}> \\
4k^2+4k+1 \\
\equiv\, <\mathrm{algebra}> \\
2(2k^2+2k)+1 \\
\equiv\, <\mathrm{substitution}> \\
2r+1
\end{flalign}
$$

What if we skip the last substitution? We can do this instead:

$$
\mathrm{let}\,r=2k^2+2k
$$

Since $k$ is an integer, $r=2k^2+2k$ is also an integer. $\therefore n^2$ can be written as $2r+1 \therefore$ by the definition of odd integers, $n^2$ is odd.

## Example 2: Give a direct proof of the theorem "The sum of two real rational numbers is rational"

Remember the definition of a rational number:
![[Definitions.md#Rational Number]]

### Proof:

Arbitrarily pick 2 rational numbers.
$\mathrm{let}\, r$ and $s$ be two real rational numbers.
$\therefore$ there exist integers $p,q,t,u$ ($q\neq0$ and $u\neq0$ such that $r=\frac{p}{q}$ and $s=\frac{t}{u}$).

Now,

$$
\begin{split}
r+s \\
\equiv < subt> \\
\frac{p}{q} + \frac{t}{u} \\
\equiv <algebra> \\
\frac{pu+tq}{qu}
\end{split}
$$

Let $u$ = $pu+tq$ and $w=qu$.
Since $p,q,t,u$ are integers & $q\neq 0$ and $u\neq 0$, $u$ and $w$ are integers and $w\neq0$.
$\therefore$ by definition of rational numbers, $r+s$ is rational.
