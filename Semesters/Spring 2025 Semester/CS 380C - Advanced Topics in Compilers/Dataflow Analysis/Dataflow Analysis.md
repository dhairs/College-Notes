## What is it

When optimizing programs, we need to know the way data is passed through functions and different branches. This is important in making sure that the optimized program is the equivalent to the original program.

## Inference Rules Extended

This extends the first, follow, and nullable sets we learned [[Inference Rules|earlier]].

### Follow
$\$\in \text{FOLLOW}(S)$

$\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{\$\}$

The follow set is the [[Power Set|power set]] of $T$ terminals, and thus has $2^T$ elements.