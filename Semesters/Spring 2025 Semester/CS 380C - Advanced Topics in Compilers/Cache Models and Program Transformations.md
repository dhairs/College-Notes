## Memory Wall Problem

Optimization focus so far has been reducing the [[Scalar Optimizations|amount of computation]]. However, on modern machine, most programs that access a lot of data are memory bound. The latency of [[Main Memory#DRAM|DRAM]] is usually on the order of 100-1000 cycles.

Caches can reduce the effective latency of memory access, but programs may need to be rewritten to take full advantage of caches. 

## Do Cache Optimizations Matter?

This is best shown by way of [[Matrix Multiplication]]. Because matrix multiplication requires multiple passes over the same memory addresses, there is a lot of space for cache optimization.

| ![[matrix multiply opt.png]]                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------- |
| https://medium.com/@Styp/why-loops-do-matter-a-story-of-matrix-multiplication-cache-access-patterns-and-java-859111845c25 |

## Two Key Transformations

### Loop Interchange/Permutation

```pseudocode
for I ...
	for J ...
		S(I,J);
```

could possibly become:

```pseudocode
for J'
	for I'
		S'(I',J')
```

### Loop Tiling/Blocking

Intuition: interleave `I` and `J` executions:

```pseudocode
for I...
	for J...
		S(I,J)
```

could possibly become:

```pseudocode
for BI...
	for BJ...
		for I'
			for J'
				S'(BI,BJ,I',J')
```

### Questions

Are these transformations legal?

Is it profitable to perform these transformations?

> [!FAQ]+ Is it profitable to perform these transformations?
> If so, how can we perform them?


## Matrix-Vector Product

Imagine the following code:

```c
for i = 1,N
	for j = 1,N
		y(i) = y(i) + A(i,j) * x(j)
```


| ![[matrix vector product.png]]                                       |
| -------------------------------------------------------------------------- |
| https://www.cs.utexas.edu/~pingali/CS380C/2025/lectures/Cache%20Models.pdf |

### Cache Abstractions

Real caches are very complex, science is all about tractable and useful abstractions (models) of complex phenomena—models are usually approximations. We'll assume a two level memory model: single-level-cache + memory.

### Stack Distance

Lets say $r_{1}$ and $r_{2}$ are two memory references where $r_{1}$ occurs earlier than $r_{2}$. $\text{stackDistance}(r_{1},r_{2})$: number of distinct cache lines referenced between $r_{1}$ and $r_{2}$. 

### Modeling Approach

Our first approximation is to ignore conflict misses and only consider cold and capacity misses.

Most problems have the notion of problem size. How does the cache miss ratio change as we increase problem size?

We can often estimate miss ratios at two extremes:
- **Large Cache Model**: problem size is small compared to cache capacity
- **Small Cache Model**: problem size is large compared to cache capacity

#### Large Cache Model

No [[Cache Performance#Capacity Miss|capacity misses]], only [[Cache Performance#Compulsory Miss|cold misses]]. 

#### Small Cache Model

[[Cache Performance#Compulsory Miss|Cold misses]] and [[Cache Performance#Capacity Miss|capacity misses]].

### Scenario 1

Lets say we have an IJ loop for performing Matrix-vector products.

The cache line size is 1 number. 

In the **large cache model**, misses