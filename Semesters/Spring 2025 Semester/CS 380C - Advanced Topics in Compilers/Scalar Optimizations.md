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

### Algebraic Simplification

More general use of constant folding. Takes advantage of usual simplification rules.
- `a * 1` can be `a`
- `a / 1` can be `a`
- `b || false` can be `b`
- etc. (just repeat these types of rules recursively)

You have to be very careful with floating point because it is [[Floating Point Numbers#Rounding|not associative]].

### Copy Propagation

After assignment `x = y`, replace uses of `x` with `y` until `x` is assigned again.

If there was an assignment `y = z` before, just transitively apply replacements.

### Common Subexpression Elimination

If program computes same expression multiple times, you can reuse the computed value.

Ex:

```c
a = b + c;
c = b + c;
d = b + c;
```

Can be turned into 

```c
a = b + c;
c = a;
d = b + c;
```

We need to track the flow of the computation (data flow analysis) to make sure we only eliminate equivalent expressions.

Common subexpressions also occur in low-level code in address calculations for array accesses:
`a[i] = b[i] + 1;`

### Unreachable Code Elimination

Not the same as dead code necessarily.

Eliminate code that is never executed.

Ex:

```c
#define debug false
int s = 1;
if(debug) printf('%d', s);
```

### Dead Code Elimination

If the effect of a statement is never observed, eliminate the statement. This is not unreachable code, but rather code that has no effect on the output.

A variable is dead if value is never used after definition.

Eliminate assignments to dead variables. Other optimizations may also create dead code.

### Loop Optimizations

Program hot spots are usually loops, exceptions usually include OS kernels and compilers.

Most of the execution time in most programs is spent in loops: 90/10 is typical.

Loop optimizations are important to reduce this.

### Loop-Invariant Code Motion

One of the most important optimizations for loops.

If the result of a statement or expression does not change during the loop, and has no *externally visible side effect*, we can hoist its computation outside of the loop.

Often, this is useful for array element addressing computations, invariant code is not visible at the source level.

This *can be unsafe*, if the loop is never going to run, and the hoisted computation is exception prone, then we possibly have an issue.

### Strength Reduction

Replaces expensive operations (multiplies, divides) by cheap ones (adds, subtracts). This is more effective in loops.

The **induction variable** is a loop variable whose value is linearly dependent on the iteration number.

Ex:

```c
s = 0;
for (i = 0; i < n; i++) {
	v = 4 * i;
	s = s + v;
}
```

Can be turned into

```c
s = 0; v = -4;
for (i = 0; i < n; i++) {
	v = v + 4;
	s = s + v;
}
```

### Induction Variable Elimination

If there are multiple induction variables in a loop, can eliminate the ones that are used only in the test condition. Thus, we need to rewrite the test using other induction variables. This is usually applied after strength reduction.

Ex:

```c
s = 0; v = -4;
for (i = 0; i < n; i++) {
	v = v + 4;
	s = s + v;
}
```

Can be turned into

```c
s = 0; v = -4;
for (; v < (4 * (n-4));) {
	v = v + 4;
	s = s + v;
}
```

### Loop Unrolling

Execute loop body multiple times at each iteration.

Ex:
```c
for (i = 0; i < n; i++) { S }
```

Can be turned into 

```c
for (i = 0; i < n - 3; i += 4) { S; S; S; S; }
for (; i < n; i++) { S; }
```

This can get rid of $\frac{3}{4}$ of conditional branches. **This is basically irrelevant in modern processors because of powerful branch predictors.**
