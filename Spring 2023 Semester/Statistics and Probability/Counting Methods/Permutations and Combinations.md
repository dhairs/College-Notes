# Permutations and Combinations

The biggest question to ask when deciding which one is being used is "does order matter?"

## Ex: Stock Portfolio

**Suppose there are 100 possible stocks**

- You want to invest equally in five stocks (20% in each). How many possible portfolios are there? (**Order doesn't matter here**)
- You want to form a 30%/25%/20%/15%/10% weighted portfolio of five stocks. How many possible portfolios are there? (**Order *does* matter here**)

## Permutations

An **ordered** subset of distinct choices is called a permutation, and $P_{n,k}=\text{num. of permutations of size}\;k \;\text{that can be formed from}\;n\; \text{objects}$ 

**General formula**: $n$ factorial over $(n-k)$ factorial ^72d40c

$$
P_{n,k}=\frac{n!}{(n-k)!}
$$

## Combinations

An **unordered** subset of choices is called a combination, and $C_{n,k}=\text{num. of combinations of size}\;k \;\text{that can be formed from}\;n\; \text{objects}$

Often written as $C_{n,k}$ can be written $\Bigl({n\atop k}\Bigl)$, which can be read as "$n$ choose $k$"

**General Formula**:
$$
C_{n,k}=\Bigl({n\atop k}\Bigl)=\frac{n!}{(n-k)!k!}
$$

## Sampling with Replacement

There are total $n$ different elements in a population or set, you want to create an ordered arrangement of $k$ elements.

If you pick an element, note it, and put it back, you are sampling with replacement.