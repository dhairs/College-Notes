
## Algorithmic Efficiency

Typically, computational problems correspond to an infinite family of instances. 

If we have some comparison sorting algorithm on $n$ distinct keys, then there are infinitely many possible values of $n$, and for each value of $n$, there's $n!$ instances.

We want to inspect how many comparisons a correct algorithm makes in the **worst case**.

A lot of the time, you can't get something that is optimal even in the worst case, so we want an algorithm that is **asymptotically efficient**.

## Quadratic Sorting Algorithms

Algorithms like insertion, selection, and bubble sort are *quadratic* sorting algorithms.

$$
\sum_{i=1}^m=i \rightarrow \theta(m^2)
$$

## Subquadratic Sorting Algorithms

Suppose we only know about quadratic sorting algorithms like insert, selection, or bubble sort. It's natural to find out whether or not a subquadratic sorting algorithm exists, but how can we express this question using asymptotic notation?