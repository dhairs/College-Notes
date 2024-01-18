## What is Probability?

Can be defined as the likelihood of an outcome occurring. **Alternatively**, it can be defined as the proportion of times an event will occur if the experiment is repeated over and over again under the same conditions. 

Written as $\frac{\text{num. of favorable outcomes}}{\text{num. of total possible outcomes}}$

Easiest to be understood in a few examples:

### Ex: Imagine a coin flip 🪙

There are two equally likely outcomes: heads or tails (assuming the coin doesn't land on its edge)

Therefore, both have a likelihood of $\frac{1}{2}=0.5$


### Ex: Imagine rolling a die 🎲

There are 6 possible outcomes: 1, 2, 3, 4, 5, 6.

Therefore, the probability of rolling a 2 is: $\frac{1}{6}$

However, the probability of rolling an even number is $\frac{3}{6}$ because there are 3 possible even numbers, and 6 possible total numbers.

## What is an Experiment and Event

- A **random experiment** is a process that can have more than one possible outcome, where the outcome itself depends on chance and cannot be specified ahead of time.
- An **event** is an outcome or a set of outcomes of an experiment.

### Simple Event
A simple event is an event that cannot be broken down further (e.g. Your coin tosses were HH, or your rolled die shows a 6)

### Compound Event
A compound event is an event that can be broken down ("decomposed") into simple events (e.g. Your coin tosses gave different results (HT), or the sum of two rolled die is 6)


## What is Sample Space?
- The sample space ($\Omega$) is the set of all possible outcomes of a random experiment.
	- Therefore, the [[Cardinality|cardinality]] of the sample space must be the # of possible outcomes.
- The different elements of a sample space must be distinct, [[#Mutually Exclusive Events|mutually exclusive]], and collectively exhaustive.

### Mutually Exclusive Events
Events that cannot occur at the same time. If one occurs, it excludes the other from occurring.

### Ex: What is the sample space for each of the following:
1. **Toss one coin**
2 outcomes ($2^1$)
$\Omega=\{\text{Heads}, \text{Tails}\}$ 
$|\Omega|=2$

2. **Roll one die**
6 outcomes ($6^1$)
$\Omega=\{1, 2, 3, 4, 5, 6\}$
$|\Omega|=6$

3. **Toss two coins together**
4 outcomes ($2^2$)
$\Omega=\{HH, HT, TH, TT\}$
$|\Omega|=4$

4. **Toss three coins together**
8 outcomes ($2^3$)
$\Omega=\{HHH, HHT, HTT, HTH, TTH, THT, THH, TTT\}$
$|\Omega|=8$

5. **Roll two dice**
36 outcomes ($6^2$) (not listed)

## [[Sets]]


## Axioms of Probability
### Non-negativity

$P(A)\geq0$ for every event $A$.

### Additivity

If $A$ and $B$ are two disjoint events, then the probability of their union satisfies $P(A\cup B)=P(A)+P(B)$.

This extends to the union of infinitely many disjoint events:
$$P(A_1\cup A_2\cup \ldots)=P(A_1)+P(A_2)+\ldots$$

### Normalization

The probability of the entire sample space $\Omega$ is equal to $1$. 

## Probability Laws

1. **If $A\subseteq B$, then $P(A)\leq P(B)$**
2. $P(A\cup B)=P(A)+P(B)-P(A\cap B)$
	1. "General Addition Rule"
	2. **If A and B are mutu**

