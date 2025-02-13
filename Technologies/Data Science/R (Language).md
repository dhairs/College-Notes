## Combinations in R

The general formula for finding a combination in `R` is:

```R
choose(n, k)
```

Go back to this example:
![[Permutations and Combinations#Ex Stock Portfolio]]

If finding the first bullet point, where order doesn't matter:

```R
choose(100, 5)
```

## Permutations in R

No built in function for permutations, but its very simple, because the equation for permutations itself is simple.

Recall the Permutation general formula:
![[Permutations and Combinations#^ee18c4]]

We can express this in `R` as:

```R
factorial(n)/factorial(n-k)
```

## Normal Distribution in R

`dnorm(x, mean, sd)` can be used to find the [[Variables#Probability Density Function |PDF]] of a normal random variable given the standard deviation and mean. It defaults to the PDF for $X~N(0,1)$

`pnorm(x, mean, sd)` can be used to find the [[Variables#Probability Density Function |PDF]] of a normal random variable given the standard deviation and mean, it defaults to the CDF for $X~N(0,1)$
