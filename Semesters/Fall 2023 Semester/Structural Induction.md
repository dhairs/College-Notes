# Example

$$\begin{align}

\exists q(x)\;\text{such that} \\
p(x) = (x-a)q(x) + p(a)\\
\exists q(x)\; \text{such that}\;p(x)=(a-a)q(x)+p(a) \\
p(x) \\
=<rec. def>\\
p_1(x)p_2(x)\\
=<IH> \\
((x-a)q_1(x)+p_1(a))((x-a)q_2(x)+p_2(a)) \\
=<algebra> \\
(x-a)^2q_1(x)q_2(x)+(x-a)q_1(x)p_2(a)+(x-a)q_2(x)p_1(a)+\bbox[teal]{p_1(a)p_2(a)} \\
=<algebra>
(x-a)\Bigl((x-a)\Bigr)

\end{align}$$




# Example
Prove that for all $n\in N$, $a^n-b^n$ is divisible by $a-b$

## Base case $n=0$
We need to show that $a^0-b^0$ is divisible by $a-b$

## Inductive
### Hypothesis
Assume $a^k=b^k$ is divisible by $(a-b)$, $k≥0$ 

### Step
We need to show that $a^{k+1}-b^{k+1}$ is divisible by $a-b$We need to show that $a^{k+1}-b^{k+1}$ is divisible by $a-b$

$$\begin{align}

a^{k+1}-b^{k+1} \\
=<algebra> \\
a\cdot a^k-b\cdot b^k \\
=<algebra> \\


\end{align}$$

We need to somehow get into the form $x(a^k-b^k)+y(a-b)$, which, when expanded, is $\bbox[teal]{xa^k}-\bbox[red]{xb^k+ya}-\bbox[green]{yb}$

So, $\b

$$\begin{align}

a^{k+1}-b^{k+1} \\
=<algebra> \\
a^{k+1}-ab^k+ab^k-b^{k+1} \\
=<algebra> \\
a(a^k-b^k)+b^k(a-b)

\end{align}$$
Thus, by $IH$ $a^k-b^k$ is divisible by $a-b$ and $(a-b)$ is also divisible by $a-b$, their addition is also divisible by $a-b$

$\therefore$ this proves the inductive step


# Example 2
## Given
$$\begin{align}
a_1=1 \\ 
a_n=a_{n-1}+3, n>1
\end{align}$$
## Prove
That the closed form of this sequence is $a_n=3n-2 \; n≥1$

## Base Case $n=1$

We need to show that $a_1=3\cdot1-2$

$$\begin{align}
a_1 \\
=<rec. def> \\
1 \\
=<arith.> \\
3\cdot1-2
\end{align}$$

$\therefore$ this proves the base case.

## Inductive
### Hypothesis
Assume $a_k=3k-2\; k≥1$

### Step
We need to show that $a_{k+1}=3(k+1)-2$

$$\begin{align}
a_{k+1} \\
=<rec. def> \\
a_k+3 \\
=<IH> \\
3k-2+3 \\
=>algebra> \\
3(k+1) -2
\end{align}$$