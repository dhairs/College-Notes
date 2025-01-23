## Definition

A context free grammar consists of:
- A set of non-terminals $N$ ^56b2d0
	- A symbol that can be rewritten into other symbols.
- A set of terminals $T$ ^f9b1d7
	- A symbol that can no longer be rewritten into other symbols.
- A start symbol $S$
- A set of productions $P$

Each context-free grammar has an empty-string:
- A null-symbol $\epsilon$

Recursive rules means the language can generated an unbounded number of variations of sentences (ex. $E\to E+E$ is recursive).

If you, given the string, can get to the final string given the grammar, it is a part of the language.

## Ambiguity

## Grammar

Is a grammar that can create *even a single* sentence with multiple parse trees given an input.

### Ambiguous Languages

A language that, no matter what grammar generated it, is ambiguous. This means that *every* grammar that generated it must be ambiguous.

## How to use

1. Begin with a string with the start symbol
2. Replace any non-terminal $X$ in the string by a right-hand side of some production $X\rightarrow Y_{1}\dots Y_{n}$
3. Repeat until eventually at a string consisting of only terminal symbols.