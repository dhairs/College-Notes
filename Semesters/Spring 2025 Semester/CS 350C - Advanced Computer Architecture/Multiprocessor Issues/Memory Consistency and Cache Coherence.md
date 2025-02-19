Part of the multiprocessor issues lessons.
## Shared Memory Parallelism

There are multiple processor cores, each of which may read and write to a single shared address space.

> [!FAQ] What does correctness of such a shared memory system mean?
> Memory consistency
> Cache Coherence

## Consistency vs. Coherence

**Consistency** is a precise, architecturally visible definition of shared memory correctness. This provides rules about loads and stores and how they act upon memory. It also usually allows many correct executions while disallowing many more incorrect ones

**Coherence** is a microarchitectural means to supporting a consistency model. In a shared-memory system with caches, the cached values can potentially become out-of-date (or *incoherent*) when one of the processors updates its cached copy of a shared value. Coherence seeks to make the caches of a shared-memory system as functionally invisible as the caches in a single-core system by propagating one processor's write to other processor's caches.

Coherence issues arise because of one fundamental issue: there exist multiple actors with acces

### Example of Incoherence

| Time | Core C1    | Core C2             |
| ---- | ---------- | ------------------- |
| 1    | S1: A = 43 | L1: while (A == 42) |
| 2    |            | L2: while (A == 42) |
| 3    |            | L3: while (A == 42) |
| 4    |            | ...                 |
| 5    |            | Ln: while (A == 42) |

If the change in Core C1 is not eventually made visible, Core C2 will keep running forever. That is not a designed, nor desirable outcome.

## Baseline System Model

All cores can perform loads and stores to all **physical** addresses.

Each core is single threaded.

Each core has a private, write back, physical index, physical tag (PIPT) D$ (cache [[Cache Organization]]).


