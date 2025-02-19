Part of the multiprocessor issues lessons.
## Shared Memory Parallelism

There are multiple processor cores, each of which may read and write to a single shared address space.

> [!FAQ] What does correctness of such a shared memory system mean?
> Memory consistency
> Cache Coherence

## Consistency vs. Coherence

**Consistency** is a precise, architecturally visible definition of shared memory correctness. This provides rules about loads and stores and how they act upon memory. It also usually allows many correct executions while disallowing many more incorrect ones

**Coherence** is a microarchitectural means to supporting a consistency model. In a shared-memory system with caches, the cached values can potentially become out-of-date (or *incoherent*) when one of the processors updates its cached copy of a shared value. Coherence seeks to make the caches of a shared-memory system as functionally invisible as the caches in a single-core system by propagating one processor's write to other processor's caches.

Coherence issues arise because of one fundamental issue: there exist multiple actors with access to caches and memory. In modern systems, these actors are processor cores, DMA engines, and external devices that can read and/or write to caches and memory.

### Example of Incoherence

| Time | Core C1    | Core C2             |
| ---- | ---------- | ------------------- |
| 1    | S1: A = 43 | L1: while (A == 42) |
| 2    |            | L2: while (A == 42) |
| 3    |            | L3: while (A == 42) |
| 4    |            | ...                 |
| 5    |            | Ln: while (A == 42) |

If the change in Core C1 is not eventually made visible, Core C2 will keep running forever. That is not a designed, nor desirable outcome.

If a chance by Core C1 to A's value in its cache is not made visible to 

## Baseline System Model

| ![[Baseline Model.png]]                                                          |
| -------------------------------------------------------------------------------- |
| Figure 2.1 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

All cores can perform loads and stores to all **physical** addresses.

Each core is single threaded.

Each core has a private, write back, physical index, physical tag (PIPT) D$ (cache [[Cache Organization]]).

## Pipeline-Coherence Interface

| ![[Pipeline Coherence Interface.png]]                                             |
| -------------------------------------------------------------------------------- |
| Figure 2.2 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

Informally, a coherence protocol must ensure that writes are made visible to all processors. The processor cores interact with the coherence protocol through a coherence interface with two methods:
- A read-request method
- A write-request method

A coherence protocol can be either consistency-agnostic or consistency-directed. 

In a **consistency-agnostic** protocol, a write is made visible to all other cores before returning (i.e., writes are propagated synchronously). The interface becomes that of an atomic memory system with no caches present.

In a **consistency-directed** protocol, a write can return before it has been made visible to all cores (i.e., writes are propagated asynchronously). These emerged to support throughput-based GP-GPUs and heterogeneous systems.

### Consistency-Agnostic Coherence Invariants

We need two variants to describe this approach:
- Single-Writer, Multiple Read (SWMR) Invariant
- Data-Value Invariant

| SWMR                                                                                                                                                         | Data-Value                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| For any memory location A, at any given time, there exists only a single core that may write and read to A **or** some number of cores that may only read A. | The value of the memory location at the start of an epoch is the same as the value of the memory location at the end of its last read-write **epoch**. |

## Consistency

### Sequential Consistency (SC)

A single core is **sequential** if the "result of an execution is the same as if the operations had been executed in the order specified by the program."

A multiprocessor is **sequentially consistence** if "the result of any execution is the same as if the operations of **all** cores were executed in **some** sequential order, and the operations of each individual core appear in this sequence in the order specified by its program."

| [Lamport 1979](https://ieeexplore.ieee.org/document/1675439) |
| ------------------------------------------------------------ |

The total order of operations is called **memory order**. In sequential consistency, memory order $<_{m}$ respects each core's program order $<^{c}_{p}$.
