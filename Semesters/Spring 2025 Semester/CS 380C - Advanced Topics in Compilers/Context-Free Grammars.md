## Definition

A context free grammar consists of:
- A set of non-terminals $N$
- A set of terminals $T$
- A start symbol $S$

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
3. Repeat
4. 