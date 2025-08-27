## Stable Marriage Problem

In its most basic version, we are given $n$ men and $n$ women. Each man has complete, strict preferences over the $n$ women, and each woman has complete, strict preferences over the $n$ men.

Any collection of disjoint man-woman pairs will be referred to as a matching. A matching is considered **perfect** if it consists of $n$ pairs (i.e. it matches all of the men and women).

The objective is to compute a "good" perfect matching.

### What Constitutes a **Good** Perfect Matching?

Ideal situation would be where we could give each man/woman their first choice. This isn't always possible.

We need to identify an interesting notion of 'good' that is always achievable.

We'll first identify a natural class of "defects" to avoid in our solution. A good perfect matching will be one that does not have these defects.

### Useful Notation

Let $\mu$ be a matching (not necessarily perfect). For any man $m$, we write $\mu(m)$ to denote the match of $m$ under $\mu$. If $m$ is unmatched, $\mu(m)$ is 0.

We do the same for women, where women are denoted as $w$ instead of $m$.

### Blocking Pairs (Unstable Matching)

Let $\mu$ be a matching, we say that man $m$ and woman $w$ form a blocking pair with respect to $\mu$ if the following two conditions hold:
- Man $m$ prefers woman $w$ to $\mu(m)$
- Woman $w$ prefers man $m$ to $\mu(w)$

If $\mu$ admits such a blocking pair then we say that $\mu$ is unstable.

### Stable Matchings

We define a stable matching as a perfect matching with **no blocking pair**.

Does every instance of the stable marriage problem admit a stable matching? If so, can we compute a stable matching efficiently (or even compute the existence of a stable matching efficiently)?

## Gale-Shapley Proposal Algorithm

- Initialize $\mu$ to the empty matching.
- While some man is single,
	- Let $m$ be an arbitrary single man
	- Man $m$ proposes to the highest-ranked woman $w$ on his preference list to whome he has not already proposed
	- If woman $w$ prefers man $m$ to her current match (which could be 0)
		- If woman $w$ is currently matched with some man $m'$, then the pair $(m',w)$ is removed from $\mu$
		- The pair $(m,w)$ is added to $\mu$

### Properties of the Gale-Shapley Proposal Algorithm

Throughout the execution of the algorithm, $\mu$ is a matching. If the algorithm terminates, then it produces a perfect matching. 

A woman is single until she is proposed to for the first time, thereafter, she is tentatively matched.

If a woman $w$ is tentatively matched to a man $m$, and is subsequently tentatively matched to a man $m' \neq m$, then $w$ prefers $m'$ to $m$. Essentially, a woman will never be re-matched to someone less preferable.

### Termination of Gale-Shapley Proposal Algorithm

No man makes more than $n$ proposals. Suppose a man makes an $n$th proposal, after this proposal, all $n$ women have been proposed to and as such are all tentatively matched. Thus all $n$ men are also tentatively matched. Thus no man is single, and the algorithm terminates.

The algorithm terminates within $n^2$ iterations.

### Stability of Gale-Shapley Proposal Algorithm

Let $\mu^*$ denote the output perfect matching.

Assume for the sake of contradiction that $(m,w)$ is a blocking pair for $\mu^*$. 

At some point in the execution, $m$ was rejected by $w$ in favor of a man $m'$. Furthermore, $w$ likes $\mu^*(w)$ at least as well as $m'$, since her sequence of tentative matches can only improve. Thus, $w$ prefers $\mu^*(w)$ to $m$, which is a contradiction.

There can be multiple stable outcomes.

## Man Optim