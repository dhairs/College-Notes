
## In C

Just think `malloc` and `free`. Literally you managing the memory at runtime.

## Definition

Refers to the algorithms for allocating and deallocating objects of a variable size in memory at program **execution time** (hence the "dynamic")

## Types of Management

### Explicit Memory Management

The application is responsible for freeing allocated memory
- E.g, `malloc` and `free` in C, `new` and `delete` in C++

### Implicit Memory Management

Garbage collection

### Block Diagram

- The application interacts with the allocator, which is part of the language run time environment
- At the back end, the allocator relies on certain OS services

![[Memory Allocation Block Diagram]]

### Allocator Efficiency

**Time Efficiency**: Maximize throughput (# of requests per unit time)

**Space Efficiency**: Maximize memory utilization, or, equivalently, minimize overhead or wasted space
- In general, when the application calls the allocator for $s$ bytes, the allocator responds with a pointer to a block of size $t\geq s$ bytes, so the overhead is $(t-s)$ bytes
- Overhead is for metadata

### How the Allocator "See's" it

At any instant of time, the allocator has some memory it has obtained from the OS via `sbrk()` calls
- This space is called the **pool** or **arena**

The memory is then broken up, aka **fragmented**, into variable-sized blocks of two types:
- An allocated block is one that has been given to a mutator already, so it cannot be used again `free` is called
- A free block is one that hasn't yet been allocated, it can be used by `malloc`.

![[Fragmented_Memory_Embedded.png]]

(Source: https://dmitryfrank.com/articles/heap_on_embedded_devices)

## Design of `malloc` and `free`

```c
void *malloc(size_t n) {
	m = realSize(n); // including metadata + n
	
	// find free block B with size >= m
	
	// if there is no block, call sbrk()
	if(!block) {
		sbrk();
	}
	
	// split the memory block to size
	// move the part that is for user to allocated pile
	// add the other part of memory (the extra) to the free block heap/pile
	
	return piece; // the allocated part
}
```

```c
void free(void *p) {
	// validate the block with its stored metadata
	// move block from allocated pile to free pile
	// coalesce (make it one big block to stop fragmentation)
}
```

