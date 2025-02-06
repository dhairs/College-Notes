## Why Optimize

People often don't write optimal code, we can recognize ways to improve code through analysis.

High-level languages may make some optimizations that are inconvenient to write or impossible to express. Think of incrementing the value of an array at an address: 
`a[i][j] = a[i][j] + 1;`

High-level unoptimized code may be more readable, cleaner, or modular. E.g., getting rid of method calls/jump instructions for simple methods: 
`int square(x) { return x * x };`

## Where to Optimize?

The usual goal is the improve time performance for the program. As a result, many optimizations trade off space versus time. Think about [[Introduction to Compilers#Example Matrix Multiplication|loop tiling]] for matrix multiplication.

Also, compilation time should be relatively optimized. We should optimize only program hot spots, so the program doesn't take forever to compile. 

## Possible Optimizations

Lots of possibilities to optimize programs, the most common ones include:

### Constant Propagation

If the value of a variable os known to be a constant, just replace the use of the variable with the constant. You can only do this when the variable has a known constant value.

### Constant Folding

Evaluate a constant expression if operands are known at compile time.

Ex. `x = 1.1 * 2` can be turned into `x = 2.2` at compile time.
