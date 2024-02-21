# Numerical and Categorical Variables

A variable is a *measurable* characteristic of a given unit/observation.

## What is a Random Variable

A random variable is a variable defined in the context of a random [[Overview, Definitions, and Axioms of Probability#What is an Experiment and Event|experiment]].

## Numerical Variable

A variable that has a number associated with the characteristic.

**Examples**: 
- Weekly earnings of an individual
- Daily facility production
- Annual GDP of a country

Literally anything quantifiable.

Three types of Numerical Variable:
### Discrete Variable

A variable where the number of possible values can be counted, even if the number of possible values is infinite. Think of [[Countable Sets|countability]]. Basically things like integers, those are good and discrete.

**Examples**:
- Number of children in a house hold
- Number of patents given to a firm in a year
- Number of states with a Republican governor

#### Probability Mass Function (PMF)

A probability mass function assigns probabilities to the different values that a discrete random variable can take.

Can be in a table, or function.

In general, the probability that a random variable $X$ takes a value $x$ is written as $p_x(x)$, $P_x(x)$, or $P_x(X=x)$

A random variable is always written in upper case and the numerical value we are trying to solve is always written in lower case.

#### Properties of PMF's

1. $P(X=x)\geq 0$ for all values of $x$
2. $\sum_x P(X=x)=1$ 

#### Example: PMF as a Table

$X=$ number of heads in 2 fair coin tosses
- $X$ can take values in $\{0,1,2\}$

- $P(X=0)=P(\{T,T\})=\frac{1}{4}$ 
- $P(X=1)=P(\{\{HT\},\{TH\}\})=\frac{1}{2}$ 
- $P(X=2)=P(\{H,H\})=\frac{1}{4}$ 

| $x$ | **0** | **1** | **2** |
| ---- | ---- | ---- | ---- |
| $P(X=x)$ | $\frac{1}{4}$ | $\frac{1}{2}$ | $\frac{1}{4}$ |

#### Example: PMF as a Function

$X=$ the number of rolls of a fair die until you get the first 6

$X$ can take what values?

PMF is $P(X=x)=p\times(1-p)^{n-1}$ where $n$ is the total rolls and $p$ is the probability of getting a 6

### Continuous Variable

A variable that can take on any value on some interval or intervals of the real line, including even maybe the entire line.

**Examples**:
- Monthly rainfall in Austin
- Annual GDP of the U.S.
- Daily stock return of IBM

### Approximately Continuous Variable

A discrete variable that can be treated and modeled as continuous, which is the case when the 2 following conditions are met:
1. The unit of measurement is small compared to the typical values of the variable
2. The number of values in the data set is large, with relatively few repeats

**Examples**:
- Weekly earnings of an individual
- Number of employees in a firm
- Credit score for an individual

## Categorical Variables

A variable that has two or more categories, but no obvious numerical measure associated with the characteristic.

Categorical variables may be **ordered** if there is some natural ordering of the choices (think of health status: excellent, okay, bad, terrible). They may also be **unordered** if there is no natural ordering to the choices (think of labor force status).

**Examples**: 
- Labor force status of an individual
- Health rating of an individual
- State identifier

### Binary Variables (Bernoulli Variables)

A special case of categorical variables with only two categories.

**Examples**:
- Married? (yes/no)
- Homeowner? (yes/no)
- Vaccinated? (yes/no)

### Coding categorical variables (indicator variables)

We can code categorical variables by providing a unique value to each choice in the variable.

You need $(\text{number of categories}-1)$ indicator variables.
#### Ex: Home Ownership

We can answer either yes or no, so, we can define the variable owner to be:

$$
\begin{align}
   owner=\left\{
\begin{array}{ll}
      1\;\text{if individual owns home ("yes")} \\
      0\;\text{if not ("no")} \\
\end{array} 
\right. 
\end{align}
$$

#### Ex: Labor Force Status

We have more than two options (employed, unemployed, not in labor force), so we define this as:

$$
\begin{align}
   employed=\left\{
\begin{array}{ll}
      1\;\text{if individual is employed} \\
	      0\;\text{if not (unemployed or not in LF)} \\
\end{array} 
\right. \\ \\
   unemp=\left\{
\begin{array}{ll}
      1\;\text{if individual is unemployed} \\
	      0\;\text{if not (employed or not in LF)} \\
\end{array} 
\right. \\ \\
   notInLF=\left\{
\begin{array}{ll}
      1\;\text{if individual is not in LF} \\
	      0\;\text{if not (employed or unemployed)} \\
\end{array} 
\right. 
\end{align}
$$

Note that we ended needing only 2 of these variables, because the rest is still included in the other variables.