## Stable Marriage Problem

In its most basic version, we are given $n$ men and $n$ women. Each man has complete, strict preferences over the $n$ women, and each woman has complete, strict preferences over the $n$ men.

Any collection of disjoint man-woman pairs will be referred to as a matching. A matching is considered **perfect** if it consists of $n$ pairs (i.e. it matches all of the men and women).

The objective is to compute a "good" perfect matching.

### What Constitutes a **Good** Perfect Matching?

Ideal situation would be where we could give each man/woman their first choice. This isn't always possible.

We need to identify an interesting notion of 'good' that is always achievable.

We'll first identify a natural class of "defects" to avoid in our solution. A good perfect matching will be one that does not have these defects.

### Useful Notation

Let $\mu$ be a matching (not necessarily perfect).