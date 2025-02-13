## Definition

First parsers for high-level programming languages. Had to work for the first recursive language, ALGOL.

## Two Views

### String View

Determine a leftmost derivation of the input while reading the input from left to right while looking ahead at most 1 input token. We can very easily create sets for the [[Inference Rules]] with these types of compilers.

### Tree View

Beginning with the start symbol, grow a parse tree top-down in left-to-right preorder while looking ahead at most 1 token beyond the input prefix matched by the parse tree derived so far.

## Expression Grammar

## Constructing Parsing Tables

### Easy Case

The grammar:
- has no $\epsilon$ productions
- every production begins with a terminal symbol

Easy to fill in the parsing table. If there are two or more productions in a given spot on the table, it is not SLL(1).

### Generalizing Construction (Medium Case)

What if some production s start with non-terminal symbols? Still no $\epsilon$ productions.

For each production $A\to Y_{1}Y_{2}\dots Y_{n}$
- Enter production into Table$[A,t]$ for each terminal $t$ in FIRST($Y_{1}$)

### Generalizing Construction (Hard Case)

Now we need to handle $\epsilon$ productions, but this leads to two problems:
- Where should the production $A\to \epsilon$ go in the parsing table?
	- Insert $A\to \epsilon$ into Table$[A,x]$ if $x$ in FOLLOW($A$)
- Where should $S\to Ax$ go in the parsing table?

We then enter production $A\to Y_{1}\dots Y_{n}$ into Table$[A,t]$ for all $t$ such that
- $t\in \text{FIRST}(Y_{1}\dots Y_{n})$
- $\epsilon\in \text{FIRST}(Y_{1}\dots Y_{n})$ and $t\in \text{FOLLOW}(A)$