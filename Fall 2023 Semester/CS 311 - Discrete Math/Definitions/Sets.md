# Definition
Sets are an *unordered* collection of objects.

When we say $a\in{A}$ we mean $a$ *in/belongs to* $A$.

# Roster Method
When you list out every object, similar to a literal sports roster.

i.e.: 
> $V=\{a,e,i,o,u\}$
> $E=\{2,4,6,8,\ldots,98\}$

# Set Builder

$O = \{x|x\;\text{is odd and }x<10\}$
"$x\;\text{is odd and }x<10$" is referred to as the **predicate**.

# Notation
If we say "$A$ is a subset of $B$" or that "$B$ is a superset of $A$,"  we are saying

$$(\forall{x}|x\in{A}: x\in{A}\to{x}\in{B})$$

# Theorem
for every set $S$
1. $\varnothing\le S$
2. $S\le{S}$

Proof:

let $S$ be a set. 
1. We need to show that $\varnothing\le S$. In other words, for an arbitrary $x$, if $x\in{\varnothing}$, we must show that $x\in{S}$. However, $\varnothing$ is the empty set $\therefore x\in{\varnothing}$ is false. $\therefore$ Vacuously, if $x\in\varnothing\to{x}\in{S}$ is true, $\therefore\varnothing\le{S}$
2. We need to show that $S\le{S}$. We need to show that for every element in $S$ if $x\in{S}\to{x}\in{S}$, $x\in{S}$ is always true. $\therefore$ $x\in{S}$ is always true. $\therefore S\le{S}$

![](Definitions.md#Definitions%20of%20Sets)

