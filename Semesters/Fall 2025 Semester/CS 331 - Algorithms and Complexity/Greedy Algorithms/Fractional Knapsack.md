## Knapsack Problem

In the knapsack problem, we are given a positive integer knapsack capacity $W$ and $n$ items indexed from $1$ to $n$.

Item $i$ has positive integer value $v_{i}$ and weight $w_{i}$

We wish to identify a maximum value set of items with weight at **most** $W$. 

*Note: no polynomial time algorithm is known for this problem*.

### Fractional Knapsack Variation

In the fractional knapsack problem, we are allowed to take a fractional amount of any item.

## Important Observation

Let $i$ be an item with maximum "value density" $\frac{v_{i}}{w_{i}}$.

We claim that *some* optimal solution includes a $z=\text{min}\left( \frac{1,W}{w_{i}} \right)$ fraction of item $i$.

To prove this claim, we can use an exchange argument:
- Let $S$ be an optimal solution that includes a fraction $z'<z$ of item $i$
- Observe that weight of $S$ is at least $z\cdot w_{i}$
- Modify $S$ by removing fractional items not equal to $i$ with total weight $(z-z')w_{i}$