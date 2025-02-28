## Coherence Protocols

The goal of these is to maintain coherence by enforcing coherence invariants.

Snooping protocols are simpler to specify, reason about, and implement, but harder to scale. It requires a totally ordered broadcast network and can be further optimized for non-atomic bus transactions. It's not a great fit for the era of scalable multicore systems beyond the single-chip boundary. 

Directory protocols, however, are inherently scalable and need to have a scalable way to maintain the directory to avoid creating a bottleneck. It needs to be careful to cause deadlock during message passing (e.g., by using virtual networks). Using a network that doesn't enforce point-to-point ordering (e.g., by using adaptive routing) requires a rethink of the protocol.

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

| Cache controller specification. Shaded entries are impossible and blank entries denote events that are ignored. |
| --------------------------------------------------------------------------------------------------------------- |
| ![[Cache Controller Specification.png]]                                                                         |
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
#### Transactions

| Common Transactions                                                             |
| ------------------------------------------------------------------------------- |
| ![[Common transactions.png]]                                                    |
| Table 6.4 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

| Common Core Requests to Cache Controller                                        |
| ------------------------------------------------------------------------------- |
| ![[Core requests to controller.png]]                                            |
| Table 6.4 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

### Protocol Design Options

**Snooping vs. Directory**

| Option        | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Snooping**  | A cache controller initiates a request for a block by broadcasting a request message to all other coherence controllers. Coherence controllers collectively "do the right thing." The interconnection network delivers broadcast messages in a consistent order to all core                                                                                                                                              |
| **Directory** | A cache controller initiates a request for a block by **unicasting** it to the memory controller that is the **home** for the block. The memory controller maintains a directory that holds state about each block in the LLC/memory, such as the identity of the current owner or the identities of current sharers. The memory controller forwards the message to the current owner for completion of the transaction. |

**Invalidate vs. Update**

| Option         | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Invalidate** | When a core wishes to write to a block, it initiates a coherence transaction to invalidate the copies in all other caches. Once the copies are invalidated, the requestor can write to the block without the possibility of another core reading the block’s old value. If another core wishes to read the block after its copy has been invalidated, it must initiate a new coherence transaction to obtain the block, and it will obtain a copy from the core that wrote it, thus preserving coherence. |
| **Update**     | When a core wishes to write a block, it initiates a coherence transaction to update the copies in all other caches to reflect the new value it wrote to the block.                                                                                                                                                                                                                                                                                                                                        |

#### Snooping

The basic idea is that all coherence controllers observe (**snoop**) coherence requests in the same order and collectively "do the right thing" to maintain coherence invariants. Coherence requests typically travel on an ordered broadcast network, such as a bus. This is able to **guarantee** a **total order** of **all coherence requests** (not just per-block requests), which makes it easier to implement consistency models such as [[Memory Consistency#Sequential Consistency (SC)|SC]] and [[Memory Consistency#Total Store Order (TSO) Consistency Model|TSO]] that require a total order of memory references.

| Snooping Coherence Example. All activity involves block A (denoted "A:")        |
| ------------------------------------------------------------------------------- |
| ![[Snooping coherence example.png]]                                             |
| Table 7.1 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

| Snooping Incoherence Example. All activity involves block A (denoted "A:")      |
| ------------------------------------------------------------------------------- |
| ![[Snooping incoherence example.png]]                                           |
| Table 7.2 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |
## MESI Protocol

The MESI protocol is a [[Sets|subset]] of the [[Cache Coherence#MOESI Model|MOESI protocol]].
## Snooping

The bus is in a serialized order and atomic itself, but the requests on it are not atomic.

Cache controller:

| ![[Snooping MESI.png\|400]]                                                      |
| -------------------------------------------------------------------------------- |
| Figure 7.4 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |


Memory controller: 


| ![[Snooping Memory Controller MESI.png\|400]]                                    |
| -------------------------------------------------------------------------------- |
| Figure 7.5 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

The problem with snooping is that the bus is atomic, and though it provides a totally ordered, serialized queue, it limits the speed of the cores and is hard to scale to a large amount of cores.

## Directory System Model


The directory system model looks like the following:

| ![[Directory System Model.png]]                                                  |
| -------------------------------------------------------------------------------- |
| Figure 8.1 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

The **directory** maintains a global view of the coherence state of each block. A cache controller wanting to send a `GetS` sends it directory to the directory, which then figures out what to do (which is either **respond** or **forward**). The interconnection network enforces point-to-point ordering of messages. The directory serves as the point of serialization of coherence transactions. Conflicting requests are processed by all nodes in per-block order, **not** in a total order.
- A requestor needs another strategy to determine when its request has been serialized.