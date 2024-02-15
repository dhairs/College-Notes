
# Definition

Is a complete description of the probabilities associated within the sample space $S$. 

## Ex: Rolling a six-sided die 🎲

For a fair die and $S=\{1,2,3,4,5,6\}$, the probability distribution is 

$$P(1)=P(2)=P(3)=P(4)=P(5)=P(6)=\frac{1}{6}$$

# Types of Distributions

## Marginal (unconditional) probability distributions

$P(A)$, the probability of event $A$, is also sometimes called the *unconditional probability*, or *marginal probability* of $A$

## Joint Probability Distributions

The *joint probability* of two events $A$ and $B$ is the probability that both events occur, which is $P(A\cap B)$.

## Conditional Probability Distributions

The *[[Conditional Probability|conditional probability]]* $P(A|B)$, which is the probability of event $A$ given that event $B$ has occurred, is given by:

$$P(A|B)=\frac{P(A\cap B)}{P(B)}\; \text{if}\; P(B)>0$$

### Ex: With a six-sided die 🎲

Probability of rolling at least a $3$: $A=\{3,4,5,6\}, P(A)=\frac{2}{3}$

Probability of an even roll: $B=\{2,4,6\}, P(B)=\frac{1}{2}$

The conditional probability that a roll is at least $3$ given that the roll is even:

$$P(A|B)=\frac{P(A\cap B)}{P(B)}=\frac{\frac{1}{3}}{\frac{1}{2}}=\frac{2}{3}$$

The conditional probability that a roll is even given that it is at least 3 is:
$$P(B|A)=\frac{P(A\cap B)}{P(B)}=\frac{\frac{1}{3}}{\frac{2}{3}}=\frac{1}{2}$$

## Bernoulli Distribution

A distribution based on the idea of [[Variables#Binary Variables (Bernoulli Variables)|Binary/Bernoulli Variables]]. Literally is a way of mapping the two categorical values to a function/number.

Look at [[Variables#Coding categorical variables (indicator variables)|Coding categorical variables]].

## Multiplication Rule

Comes directly from the conditional probability formula:

$$
P(A\cap B)=P(A|B)\,P(B)$$
and
$$P(A\cap B)=P(B|A)\,P(A)$$



### Ex: Product returns

Suppose a website sells three types of shirts, each with different return rates:


$$P(R|A_1)=.15$$
- Shirt 1: 60% of overall shirt sales, 15% of purchases returned  $P(A_1)=.6$
- Shirt 2: 30% of overall shirt sales, 25% of purchases returned $P(A_2)=.3$
- Shirt 3: 10% of overall shirt sales, 35% of purchases returned $P(A_3)=.1$

For a randomly selected shirt purchase, what is the probability  
that the purchase is shirt 1 and is returned?

$$P(A_1\cap R)=P(R|A_1)\,P(A_1)=(0.15)(0.6)=0.09=9\%$$

## Law of Total Probability

If $A_1, A_2, \ldots, A_k$ are disjoint events and also exhaustive events, then for any event $B$:

$$P(B)=P(B|A_1)P(A)+P(B|A_2)+\ldots+P(B|A_k)P(A_k)$$
$$=\sum^{k}_{j=1}P(B|A_j)P(A_j)$$
## Binomial Distribution

Probability of $k$ successes out of $n$ trials.

## Geometric Distribution

Number of trials to get the first success.

If $X$ is the number of trials to get the first success with $p = P(\text{success})$, then $X$ is a **Geometric Random Variable** with parameter $p$, or $X\sim \text{Geo}(p)$ 

We solve this using the **Geometric Series**.