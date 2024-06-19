![](Basic%20Equivalences.md#Law%20of%20Excluded%20Middle)

## Definition

For any statement $p$, either it is true or false. There is nothing in the middle.

So, if i want to prove $p$, I can start by assuming $\neg p$ is true.

Suppose from that I derive $F$ or any contradiction.

Basically, proof by contradiction relies on you making an assumption (a negation of part of the statement) and then proving that the statement is false when that assumption is made, then you can say that the original is true.

## Example: Prove that $\sqrt{2}$ is irrational.

Assume $\sqrt2$ is rational.
$\therefore$ There exists integers $a,b$ ($b\neq0$) such that $\sqrt2 = \frac{a}{b}$ and $a$ and $b$ have no common factors.

Now,

$$
\begin{align}
\sqrt2=\frac{a}{b}\\
\therefore <\mathrm{sq. both\; sides}>\\
2=\frac{a^2}{b^2}\\
\therefore <algebra> \\
2b^2=a^2
\end{align}
$$

Since $b$ is an integer, $a^2$ is an even integer.

$\therefore$ Using result, $a$ is even.

$\therefore$ there exists an integer $k$ such that $a=2k$

$$
\begin{align}
a=2k\\
\therefore\;<algebra>\\
2b^2=(2k)^2\\
\therefore <algebra>\\
2b^2=4k^2\\
\therefore <algebra>\\
b^2=2k^2
\end{align}
$$

Since $k^2$ is an integer, $b^2$ is even.
$\therefore$ b is even.

Since $a$ and $b$ are even, and $b$ and $a$ have a common factor of 2.

This contradicts the fact that the $a$ and $b$ are co-prime and have no common factors. Therefore, the opposite must be true, and $\sqrt{2}$ is irrational.

## Example 2: Prove a claim of the form $p\to q$ using proof by contradiction

We assume the negation $\neg(p\to q)$ and derive a contradiction.

Assume that both $p\wedge\neg q$. Derive a contradiction. We can resolve the contradiction by giving up p, but p is our premises, we will stick with $p$. Therefore, $q$ must be true. Therefore, $p\to q$.

## Example 3: Prove "for any integer $n$, if $3n+2$ is odd, then $n$ is odd"

For the negation, we assume that $n$ is even and $3n+2$ is odd.

Since $n$ is even, there exists an integer $k$ such that $n=2k$.

Now,

$$
\begin{align}
3n+2\\
\equiv<substitution>\\
3(2k)+2\\
\equiv<algebra>\\
6k+2\\
\equiv<algebra>\\
2(3k+1)
\end{align}
$$

Since $3k+1$ is an integer, $3n+2$ is even, this contradicts the fact that $3n+2$ is odd.

$\therefore n$ must be odd.

$\therefore$ by contradiction, if $3n+2$ is odd, then $n$ is odd.
