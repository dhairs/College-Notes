
# Definition

If $A_1, A_2, \ldots, A_k$ are mutually exclusive and exhaustive events, then for any event $B$,

$$P(A_i|B)=\frac{P(A_i\cap B)}{P(B)}=\frac{P(B|A_i)\,P(A_i)}{\sum^{k}_{j=1}P(B|A_j)\,P(A_j)}$$
Where $P(A_i)$ is the *prior probability* of the event $A_i$, which means this is the unconditional probability before considering additional information. 

And where $P(A_i|B)$ is the *posterior probability* of the event $A_i$, meaning that the event probability has been updated to take into account the information that event $B$ has occurred.
- Adding additional information (conditioning) is called *Bayesian Updating*.