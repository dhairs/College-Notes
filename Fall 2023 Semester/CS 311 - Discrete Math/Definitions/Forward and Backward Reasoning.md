## Forward Reasoning

- You need a starting point for a proof
- Start from your premises, apply definitions, theorems, axioms, and make way towards the conclusions

## Backward Reasoning

Start with the conclusion, and try to work backwards.

> To prove $q$, we try to find some property $p$ that we can then use to prove $p\to q$

### Example (Backward Reasoning): Given two positive real numbers $x$ and $y$, their arithmetic mean is $\frac{x+y}{2}$, and geometric mean is $\sqrt{xy}$. Prove that $\frac{x+y}{2}>\sqrt{xy}$ for two distinct positive real numbers

**NOTE: THIS IS BACKWARD REASONING, IT IS NOT A PROOF**

$$
\begin{align}
\frac{a+b}{2}>\sqrt{ab} \\
\therefore<\text{Squaring Both Sides}>\\
(\frac{a+b}{2})^2>ab\\
\therefore <algebra> \\
(\frac{a^2+2ab+b^2}{4})^2>ab \\
\therefore <algebra>\\
(a^2+2ab+b^2)>4ab\\
\therefore <algebra> \\
(a^2-2ab+b^2)>0\\
\therefore<algebra>\\
(a-b)^2>0
\end{align}
$$
