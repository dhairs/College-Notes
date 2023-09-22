## Definition
This is a type of [[Proof by Cases]]
![[Proof by Cases#Definition]]

- Some theorems can be proved by examining a small number of examples
- We call this exhaustive proofs
- Better for computers, but even those have limits

## Common Errors
![[Proof by Cases#Common Errors]]
#### Example: It is true that every non-negative integer is the sum of 18 fourth power integers.

$Sol^n$: To determine if a non-negative integer can $n$ can be written as a sum of 18 fourth powers, we might begin to examine whether $n$ is the sum of 18 fourth power integers for the smallest non-negative integers.

Fourth power integers: $0,1,16,81$.

We can show that non-negative integers add up to ?? can be written as a sum of 18 fourth powers.

One might conclude it is possible based on this example, but 79 cannot be written as a sum of 18 fourth powers.

### Example: Prove that $(n+1)^3≥3^n$ if $n$ is a positive integer such that $n≤4$

#### Proof:
$n$ is a positive integer where $n≤4$. Therefore, $n=1,2,3\;\text{or}\;4$

For $n=1$
$$\begin{align}
3^1\\
\equiv<arithmetic>\\
3
\end{align}$$
And
$$\begin{align}
(1+1)^3\\
\equiv<arithmetic>\\
2^3\\
\equiv<arithmetic> \\
8
\end{align}$$
Since, $8≥3$, therefore, for $n=1$, $(n+1)^3≥3^n$.
Repeat this line of reasoning for $n=2,3,4$