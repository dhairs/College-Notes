## Definition

Once we have a frontend, we want to reach a point where we can optimize our code. We can already parse and understand characters, but we need a way to represent our code, loops, etc., in order to optimize further.

This is somewhere between high level code and real, assembly code.

There are two kinds:
- **HIR** (High-Level IR): language independent, closer to language.
- **LIR** (Low-Level IR): machine independent, closer to machine.

This way, we can get rid of the need to have a unique compiler for each language-architecture combination. We can just have a specified high- and low- level IR, and allow languages to have a front end that compiles to one of those.

## High-Level IR

Consists of a tree-node structure (ASTs). Includes high level constructs that are common to many languages: expression nodes, statement nodes, etc. 

May also have things like loops, break and continue, switch statements, etc.

## Low-Level IR

Low level representation is essentially an [[Instruction Set Architectures|instruction set]] for an abstract machine.

Representations of IR:
- Three Address Code (quadruples)
- Tree Representation
- Stack Machine (like Java bytecode)

### Three-Address Code

`a = b OP c`

Has at most three addresses, but can have fewer. Also named quadruples (a, b, c, OP). Create temporary variables and solve with binary OPs.

Allows labels and jumps. Additionally, supports function calls.

## How to Translate

Very similar to [[Recursive Descent Parsers]]. It could also support that depending on the language. 

Have a way of parsing, and then take your AST and convert each node into an IR representation. This is defined by the compiler itself, similar to how it is done for the SaM compiler.
