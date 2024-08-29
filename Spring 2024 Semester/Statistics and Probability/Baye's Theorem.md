# Definition

If $A_1, A_2, \ldots, A_k$ are mutually exclusive and exhaustive events, then for any event $B$,

$$P(A_i|B)=\frac{P(A_i\cap B)}{P(B)}=\frac{P(B|A_i)\,P(A_i)}{\sum^{k}_{j=1}P(B|A_j)\,P(A_j)}$$
Where $P(A_i)$ is the _prior probability_ of the event $A_i$, which means this is the unconditional probability before considering additional information. ^750841

Note that the denominator in the Baye's theorem rewrite utilizes the [[Total Probability Theorem]].

And where $P(A_i|B)$ is the _posterior probability_ of the event $A_i$, meaning that the event probability has been updated to take into account the information that event $B$ has occurred.

- Adding additional information (conditioning) is called _Bayesian Updating_.

## Ex: Disease Testing False Positives

Assume:

- A disease affects 2% of the population
- The false positive rate is 1%
- The false negative rate is 5%

If you test positive, we want to know:

**Given that you tested positive, what is the chance you have the disease**?

**Let** T: Test Positive, D: Have Disease

$P(D)=0.02,\;\; P(T^\complement|D)=0.05,\;\; P(T|D^\complement)=0.01$

We are trying to find $P(D|T)$.

Baye's rule gives us:

$$
\begin{align}
P(D|T)=\frac{P(T|D)P(D)}{P(T|D)P(D)+P(T|D^\complement)P(D^\complement)}
\end{align}
$$

Plugging in the numbers above we finally land at $P(D|T)=0.66$.
