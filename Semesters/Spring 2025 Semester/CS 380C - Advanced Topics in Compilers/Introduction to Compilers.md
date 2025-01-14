## Why do we need compilers?

There are two views: the traditional view and the modern view.

**Traditional View**:
- Translation: high-level language (HLL) programs to low-level machine code
- Optimization: reduce number of arithmetic operations by optimizations like common subexpression elimination (and stuff like loop invariant elimination)
- Ignore data structures: too complex to analyze
	- looked at as if it is a collection of scalar values

**Modern View**:
- Collection of automatic techniques for extracting meaning from and transforming programs
- Useful for. debugging, optimization, verification, detecting malware, translation, etc...
- Optimization:
	- Restructure (organize) computation to optimize locality and parallelism
	- Reducing amount of computational is useful but not critical
	- Optimizing data structure accesses is critical
		- Now, we look at data structures as their own entities, and understand accesses to the structure

### Example Optimization

Prefix sum problem. Do a divide and conquer algorithm (SCAN). It would be $O(\log N)$ time instead of $O(N)$.

## Why do we need translators?

- Bridge the "semantic gap"
	- Programmers prefer to write programs at a high level of abstraction
- Application portability
	- Compilers can just recompile for different ISAs

## Getting Performance

Programs must exploit 
- coarse-grain (thread-level) parallelism
- memory hierarchy
- instruction-level parallelism (ILP)
- registers
- etc...

How important is it to exploit these hardware features?
- If you have $n$ cores and only run on one, you get at most of $\frac{1}{n}$ of peak performance

## Software Problem

The problem is that:
- Programs obtained by expressing most algorithms in the straightforward way may perform poorly
- Worrying about performance when coding algorithms complicates the software process a lot

Caches are useful only if programs have locality of reference
- temporal locality: program references memory addresses many times within a small period
- spatial locality: program references in address space are clustered in time (e.g., iterating sequentially over an array)

### Example: Matrix Multiplication

```pseudocode
for I = 1, n
	for J = 1, n
		for K = 1, n
			C(I,J) = C(I,J) + A(I,K) * B(K,J)
```

*Note: this assumes the arrays are stored in row-major order*

- All six permutations of these loops are computationally equivalent
- Great algorithmic data reuse: each array element is touched $O(N)$ times
- Execution times of the six 