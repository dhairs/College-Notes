## Definition

First parsers for high-level programming languages. Had to work for the first recursive language, ALGOL.

## Two Views

### String View

Determine a leftmost derivation of the input while reading the input from left to right while looking ahead at most 1 input token

### Tree View

Beginning with the start symbol, grow a parse tree top-down in left-to-right preorder while looking ahead at most 1 token beyond the input prefix matched by the parse tree derived so far.

## Expression Grammar

