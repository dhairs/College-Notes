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