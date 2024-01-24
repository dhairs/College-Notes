## Statistical Independence

If knowing $B$ doesn't give you any information to the probability of $A$ occurring, then $A$ and $B$ are **independent**.

Thus: 

$$\text{if}\; P(A|B)=P(A)$$
The events $A$ and $B$ are independent.


$A$ and $B$ are independent $\text{iff}\; P(A\cap B)=P(A)P(B)$

If the events $A$ and $B$ are independent, $P(A|B^\complement)=P(A)$ 

### Checking for Independence
#### Method 1
Check $P(A|B)=P(A)$ or $P(B|A)=P(B)$
#### Method 2
Check $P(A\cap B)=P(A)\,P(B)$
## Statistical Dependence

If knowing $B$ provides some information on the probability of $A$ occurring, then $A$ and $B$ are **dependent**.

Thus:

$$\text{if}\; P(A|B)\neq P(A)$$
The events $A$ and $B$ are dependent.

## Independence of more than two events

The events $A_1,A_2,\ldots,A_k$ are *mutually independent* if, for *any* subset of the events, the joint probability is equal to the product of the individual probabilities.

Similarly, the conditional probability for any event $A_i$ given any subset of the other events is equal to the unconditional probability of $A_i$.

### Ex: 50 events

$$
\begin{align}
P(A_1\cap A_2)=P(A_1)\,P(A_2)\;\text{and similarly for any 2 events in}\; \{A_1, \ldots, A_{50}\} \\
P(A_1\cap A_2\cap A_3)=P(A_1)\,P(A_2)\,P(A_3)\;\text{and similarly for any 3 events in}\; \{A_1, \ldots, A_{50}\} \\
\ldots \\
\ldots \\
\ldots \\
P(A_1\cap A_2\cap \ldots\cap A_3)=P(A_1)\,P(A_2)\,\ldots\,P(A_{50})
\end{align}
$$
