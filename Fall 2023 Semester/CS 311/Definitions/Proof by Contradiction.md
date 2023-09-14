![[Basic Equivalences#Law of Excluded Middle]]

For any statement $p$, either it is true or false. There is nothing in the middle.

So, if i want to prove $p$, I can start by assuming $\neg p$ is true.

Suppose from that I derive $F$ or any contradiction.

### Example: Prove that $\sqrt{2}$ is irrational.
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
\therefore\;2b^2=(2k)^2\\
\therefore <algebra>\\
2b^2=4k^2\\
\therefore <algebra>\\
b^2=2k^2
\end{align}
$$
