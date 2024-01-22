
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

The *conditional probability* $P(A|B)$, which is the probability of event $A$ given that event $B$ has occurred, is given by:

$$P(A|B)=\frac{P(A\cap B)}{P(B)}\; \text{if}\; P(B)>0$$

### Ex: With a six-sided die 🎲

Probability of rolling at least a $3$: $A=\{3,4,5,6\}, P(A)=\frac{2}{3}$

Probability of an even roll: $B=\{2,4,6\}, P(B)=\frac{1}{2}$

The conditional probability that a roll is at least $3$ given that the roll is even:

$$P(A|B)=\frac{P(A\cap B)}{P(B)}=\frac{\frac{1}{3}}{\frac{1}{2}}=\frac{2}{3}$$

The conditional probability that a roll is even given that it is at least 3 is:
$$P(B|A)=\frac{P(A\cap B)}{P(B)}=\frac{\frac{1}{3}}{\frac{2}{3}}=\frac{1}{2}$$

### Multiplication Rule

Comes directly from the conditional probability formula:

$$
P(A\cap B)=P(A|B)\,P(B)$$
and
$$P(A\cap B)=P(B|A)\,P(A)$$



## Ex: Product returns

Suppose a website sells three types of shirts, each with different return rates:

- Shirt 1: 60% of overall shirt sales, 15% of purchases returned  
- Shirt 2: 30% of overall shirt sales, 25% of purchases returned  
-  Shirt 3: 10% of overall shirt sales, 35% of purchases returned  
!! : the event that shirt 1 is purchased (!" and !# similarly defined)  
$: the event that a purchase is returned.  
%(!! ) = .6  
%(!" ) = .3  
%(!# ) = .1
