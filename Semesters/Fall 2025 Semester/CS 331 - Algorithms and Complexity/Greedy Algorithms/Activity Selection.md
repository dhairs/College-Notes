
## Activity Selection Problem

We are given $n$ activities indexed from 1 to $n$. Activity $i$ has start time $s_{i}$ and end (finish) time $f_{i}$. We cannot participate in two activities that occur at the same time. 

We want to determine the maximum [[Cardinality|cardinality]] set of non-overlapping activities. Essentially, we want to see the maximum number of activities we can do.

## Important Observation

Let $i$ be an activity with minimum finish time. We claim that *some* optimal solution contains $i$.

To prove this claim, we can use the "exchange argument":
- Suppose $S$ is an optimal solution that does not include $i$
- Let $j$ be the first activity in $S$
- Then $(S-j)+i$ is an optimal solution that includes $i$

## Activity Selection Algorithms

### Activity Selection Greedy Algorithm

- Re-index the activities in non-decreasing order of finish time.
- Initialize $I$ to $\{1,\dots,n\}$ and $S$ to $\varnothing$.
	- Let $i$ be a minimum-index activity in $I$
	- Add $i$ to $S$
	- Eliminate from $I$ all indices $j$ such that activities $i$ and $j$ overlap

### Fast Implementation

- Re-index the activities in nondecreasing order of finish time
- Initialize $S$ to $\{1\}$ and $k$ to $1$
- For $i$ running from 2 to $n$
	- If the start time of activity $i$ is at least the finish time of activity $k$, then add $i$ to $S$ and set $k$ to $i$

