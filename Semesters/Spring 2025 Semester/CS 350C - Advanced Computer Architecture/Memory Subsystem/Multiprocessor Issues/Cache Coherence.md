## Coherence Protocols

The goal of these is to maintain coherence by enforcing coherence invariants.

### Coherence Invariants

| SWMR                                                                                                                                                         | Data-Value                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| For any memory location A, at any given time, there exists only a single core that may write and read to A **or** some number of cores that may only read A. | The value of the memory location at the start of an epoch is the same as the value of the memory location at the end of its last read-write **epoch**. |

### Coherence Controller

The mechanism we use for achieving this is a **Coherence controller**:
- A Mealy Finite-state machine with each storage structure
- *Logically*, a collection of identical but independent FSMs per memory block or cache line

The collection of the FSMs constitutes a distributed system in which controllers exchange messages with one another to ensure SWMR and data-value invariants are always maintained for all blocks.

The coherence protocol specifies the interactions between these FSMs.

### Simple Coherence Protocol

| ![[Baseline Model.png]]                                                          |
| -------------------------------------------------------------------------------- |
| Figure 2.1 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

We'll use the system model as a baseline. Make the interconnection network a **shared bus**. There are two **stable** coherence states for each cache line: **I**(nvalid) and **V**(alid).

There are also two stable coherence states for each memory block, **I** and **V**:
- **I**: All caches hold the block in state **I**
- **V**: One cache holds the block in state **V**

One **transient** cache state: $\text{IV}^\text{D}$. Moving from invalid to valid, but is waiting for data. Moving from stable state **I** to stable state **V**, waiting for a **D**ata response.

| ![[Cache Controller Specification.png]]                                                                         |
| --------------------------------------------------------------------------------------------------------------- |
| Cache controller specification. Shaded entries are impossible and blank entries denote events that are ignored. |
| Table 6.2 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf                                 |

| ![[Memory Controller Specification.png]]                                        |
| ------------------------------------------------------------------------------- |
| Table 6.3 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

### Coherence Protocol Design Space

#### Boolean Characteristics of a Cache Line

##### General Model

| Characteristic  | Meaning                                                                                                                                                                                     |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Validity**    | Has the most up-to-date value for the memory block                                                                                                                                          |
| **Dirtiness**   | The value is the most up-to-date value, this value differs from the value in the LLC/memory, and the cache controller is responsible for eventually updating the LLC/memory with this value |
| **Exclusivity** | This is the only privately cached copy of that memory block in the system                                                                                                                   |
| **Ownership**   | This controller (cache or memory) is responsible for responding coherence requests for the block                                                                                            |

##### MOESI Model

| Characteristic | Meaning                                                                                                                                                                          |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **M**odified   | Valid, exclusive, owned, potentially dirty. The block may be read or written                                                                                                     |
| **O**wned      | Valid, owned, potentially dirty, not exclusive. The cache has a read-only copy of the block and must respond to requests for the block. The LLC/memory copy is potentially stale |
| **E**xclusive  | Valid, not dirty, exclusive                                                                                                                                                      |
| **S**hared     | Valid, not exclusive, not dirty, not owned. The cache has a read-only copy of the block                                                                                          |
| **I**nvalid    | Not valid. The cache either does not contain the block or it contains a potentially stale copy that it may neither read nor write                                                |
