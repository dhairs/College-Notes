# Numerical and Categorical Variables

A variable is a *measurable* characteristic of a given unit/observation.

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

### Binary Variables

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