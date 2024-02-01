# Permutations and Combinations

The biggest question to ask when deciding which one is being used is "does order matter?"

## Ex: Stock Portfolio

**Suppose there are 100 possible stocks**

- You want to invest equally in five stocks (20% in each). How many possible portfolios are there? (**Order doesn't matter here**)
- You want to form a 30%/25%/20%/15%/10% weighted portfolio of five stocks. How many possible portfolios are there? (**Order *does* matter here**)

## Permutations

An **ordered** subset of distinct choices is called a permutation, and $P_{n,k}=\text{num. of permutations of size}\;k \;\text{that can be formed from}\;n\; \text{objects}$ 

**General formula**: $n$ factorial over $(n-k)$ factorial

$$
P_{n,k}=\frac{n!}{(n-k)!}
$$

^ee18c4

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

Therefore, for every $k$, we have $n$ options, because the option has been replaced. Therefore we have $n_1\times n_2\times n_3 \times \ldots\times n_k$ options.

**General Formula**:

$$
n^k
$$

## Sampling without Replacement (Permutations)

There are total $n$ different elements in a population or set, you want to create an ordered arrangement of all $n$ elements. This is also a permutation.

If you pick an element and don't put it back, you are sampling *without* replacement.

Therefore, we have $n$ options for our first sample, $n-1$ for our second, and so on.

**General Formula**:

$$
n!
$$
