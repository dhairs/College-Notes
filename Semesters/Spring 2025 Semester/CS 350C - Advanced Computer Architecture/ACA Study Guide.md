## Study Guide: Advanced Computer Architecture Topics

All my individual topic notes can be found [[Advanced Computer Architecture|here]]. A summary made by NotebookLM trained on  my notes is provided below:
### [[System Verilog]]

- SystemVerilog is a hardware description language (HDL) that is a successor and extension of Verilog. It addresses some common syntax issues present in the original Verilog.
- It is a concurrent language, meaning statements are always ready to execute and are evaluated whenever a signal on the right side changes.
- **Four-Valued Logic**: SystemVerilog, to accurately model hardware behavior including floating and unknown states, employs a four-valued logic system:
- 0: Represents false or a logical low.
- 1: Represents true or a logical high. Logical high, high voltage, Vdd, Vcc, "True", or "Asserted" all mean the same thing.
- z: Represents a floating or high-impedance state. This can occur when a device is not actively driven high or low.
- x: Represents an invalid or unknown state (don't know, don't care).
- SystemVerilog provides various ways to describe hardware, including:
- **Continuous Assignment**: Uses the assign keyword for continuous assignments outside always blocks, evaluated concurrently.
- **always Blocks**: These blocks define behavior that repeats. There are different types:
- always_ff: Used to model flip-flops (sequential logic) and typically uses non-blocking assignments (<=).
- always_latch: Used to model level-sensitive latches.
- always_comb: Used to model combinational logic and typically uses blocking assignments (=). Combinational logic outputs change immediately based on inputs.
- SystemVerilog allows for the modeling of various digital logic components, from basic logic gates (AND, OR, NOT, XOR) and multiplexers to more complex sequential elements like registers (D flip-flops) and memories.
- It supports different levels of abstraction, from structural (interconnecting components) to behavioral (describing functionality).
- SystemVerilog includes features like parameters for creating reusable and configurable modules and generate statements for defining structure in variable-sized modules.
- Test benches can be created in SystemVerilog to verify the functionality of hardware designs.

### [[Modeling and Simulating Hardware]]

- Modeling and simulating hardware are crucial steps in the design process to verify correctness before physical implementation.
- **Hardware Description Languages (HDLs)** like VHDL, Verilog, and SystemVerilog are used to create abstract models of hardware.
- VHDL (VHSIC Hardware Description Language) was initially developed under the Department of Defense for description and documentation but is also used for synthesis.
- Verilog was developed by the industry around the same time as VHDL and has a syntax rooted in C.
- SystemVerilog is an extension of Verilog that improves upon its syntax and adds features for more complex modeling and verification.
- These HDLs allow designers to describe the structure (interconnection of components) or behavior (functional operation) of digital systems.
- **Simulation** involves executing the HDL model using specialized software (simulators) to observe its behavior under various input stimuli and verify if it meets the design specifications.
- Simulation allows for the detection of design errors early in the development cycle, reducing the cost and time of debugging physical prototypes.
- Modeling can occur at different levels of abstraction, from high-level algorithmic descriptions to detailed gate-level implementations.
- **Timing and delay** can be incorporated into HDL models to simulate the real-world behavior of digital circuits, including gate delays and propagation delays. Logic gates have a propagation delay, which is the time it takes for the output to react to input changes.

### Floating Point

- Floating-point representation is a way to represent a wide range of numbers, including very large and very small values, using a fixed number of bits. This is necessary because integer representations with a fixed number of bits have a limited range.
- Floating-point numbers are crucial for scientific and engineering applications where the magnitude of numbers can vary significantly.
- The design of floating-point systems aims for efficiency in storage and computational time.

### [[Floating Point Numbers]]

- A normalized floating-point number $x$ in a system with precision $p$, exponent width $q$, and base $b$ can be represented as $x = (-1)^n \times s \times b^e$.
- $n$ represents the sign (0 for positive, 1 for negative).
- $s$ is the significand (also called mantissa or fraction). For $b=2$ and normalized numbers, there is often a hidden leading bit (usually 1) that is not explicitly stored.
- $e$ is the exponent. The exponent is often stored in a biased representation to simplify comparisons.
- $b$ is the base (radix), commonly 2.
- **Precision ($p$)** refers to the total number of digits in the significand (including the hidden bit, if applicable for $b=2$) and determines the accuracy of the representation.
- **Exponent width ($q$)** determines the range of exponents that can be represented, thus affecting the magnitude of the numbers that can be stored.
- For base $b=2$, normalized floating-point numbers often use a hidden leading '1' to the left of the binary point, increasing the effective precision by one bit.
- **Machine Epsilon ($\mathcal{E}$)** is the smallest positive number that, when added to 1, results in a value different from 1 in floating-point representation. For a precision $p$ and base 2, $\mathcal{E} = 2^{-(p-1)}$. It represents the relative precision of the floating-point system.
- The **unit in the last place (ulp)** of a floating-point number $x$ is the value of the least significant bit of its significand, scaled by the appropriate power of the base. For a normalized base-2 FP number $x = \pm S \times 2^E$, $ulp(x) = \mathcal{E} \times 2^E$. It represents the absolute gap between $x$ and the next larger or smaller representable floating-point number.
- Different floating-point systems can be defined by their $(p, q; b)$ parameters and may have specific handling of zero, subnormals, infinities, and NaNs (Not-a-Number). Some simplified systems might only include zero and normalized numbers.
- **Rounding modes** are used to determine how the result of an operation is represented when it cannot be exactly stored with the available precision.

### [[Floating Point Multiplication]]

- The multiplication of two floating-point numbers $x_1$ and $x_2$ involves the following steps:

1. **Multiply the significands ($s_1 \times s_2$)**, treating them as unsigned integers, and including any hidden bits. This might result in a significand that is twice the original precision.
2. **Add the exponents ($e_1 + e_2$)**, handling the bias used in the exponent representation. The biases need to be accounted for to get the correct unbiased exponent of the product.
3. **Determine the sign bit** of the product by XORing the sign bits of the operands ($n_1 \oplus n_2$). This is easily implemented with a combinational logic block (CLB).
4. **Normalize the product**.

- If the resulting significand is too big (e.g., greater than or equal to $2$ for base 2 due to the significand multiplication), it needs to be shifted right by one bit, and the exponent needs to be increased by one.
- If the resulting significand is too small (e.g., less than the normalized minimum, which shouldn't happen after multiplying normalized numbers unless the product is zero), it would need to be shifted left, and the exponent decreased.

1. **Handle zero**. If either operand is zero, the product is zero, and the representation needs to be adjusted accordingly.
2. **Check for exponent overflow or underflow**. If the resulting exponent is outside the representable range, an exception (e.g., infinity or underflow) needs to be generated.
3. **Round the result** to the appropriate number of bits according to the chosen rounding mode. This often requires considering guard digits, round digits, and sticky bits to make the rounding decision.
4. **Re-normalize** the product after rounding, as the rounding operation might cause the significand to become too large (e.g., $1.11...1 + 1$ could become $10.00...0$, requiring a right shift and exponent increment).

- Floating-point multiplication can be implemented using a **shift-and-add multiplier** for the significand multiplication.
- The overall process is controlled by a main control finite-state machine (FSM). The design includes an input handler, exponent adder (CLB), multiplier control (FSM), fraction shift-and-add multiplier datapath (CLB, memory), sign compute (CLB), and an output assembler. Control signals manage the flow of data between these components, such as Start, Mdone (multiplier done), Fnorm (fraction normalized), EV (exponent overflow), Load (load operands), Adx (add exponents), RSF/LSF (right/left shift fraction), Inc/Dec (increment/decrement exponent), done, and err.

### [[Memory Subsystem]]

- The memory subsystem is responsible for storing and retrieving data and instructions for the processor. It is a critical component affecting overall system performance.

### Memory Subsystem (Detailed)

- At the **device level**, the fundamental storage unit in DRAM (Dynamic Random-Access Memory) is a **1T1C cell**, consisting of one transistor and one capacitor. A United States Patent (#3,387,286) for this type of memory cell was granted to Robert H. Dennard in 1968.
- Data (a bit of information) is stored as the presence or absence of charge on the capacitor. Due to parasitic resistance, the charge on the capacitor leaks over time, necessitating periodic **refresh operations** to maintain the stored data. The refresh interval is temperature-dependent.
- **Sense amplifiers** are used to detect and amplify the small voltage difference on the bitlines caused by the charge (or lack thereof) in the DRAM cell's capacitor during a read operation. They employ a feedback loop to drive the bitlines to full logical levels ($V_{DD}$ and 0).
- **Access steps in a [[Main Memory#DRAM|DRAM]] device** involve three main phases:

1. **Sense (Open a row)**: When a row is accessed, the corresponding wordline is activated, allowing the charge from the capacitors in that row to influence the bitlines. Sense amplifiers detect this small change and amplify it. The equalization signal ($EQ$) is initially low ($E=0$), and bitlines are floating. Activating the wordline connects the capacitor to the upper bitline, causing a small voltage change (increase if the cap holds '1', decrease if it holds '0'). This starts a feedback loop that drives the bitlines to $V_{DD}$ and 0 (or vice versa).
2. **Restore and Read/Write on the opened row**: After sensing, the values in the row are restored (by keeping the wordline active for a minimum time $t_{RAS}$). For a read operation, the amplified value is connected to the output through the chip select (CS) signal. For a write operation (when write enable $WE$ is asserted), the input data is used to charge or discharge the capacitor in the selected cell. A delay $t_{RCD}$ is needed for signal stabilization before reading or writing.
3. **Precharge sense amplifiers (Close the row)**: Before another row in the same bank can be accessed, the sense amplifiers must be precharged. This involves deactivating the wordline, CS, and WE, and activating the equalization signal ($EQ$), which sets both bitlines to $V_{DD}/2$. The row precharge time $t_{RP}$ specifies the duration needed for this.

- A DRAM chip is organized as a 2D array of supercells (each containing $w$ bits), with $r$ rows and $c$ columns ($r \times c = d$, where $d \times w$ is the chip configuration, e.g., 1 Gig x 8). Access to these is managed by a **memory controller**. Modern DRAMs like DDR4 SDRAM can be internally configured with multiple banks and bank groups, each with its own sense amplifiers, to improve parallelism.
- **Programming Mode Registers** allow for the initialization and configuration of various DRAM parameters. The **SDRAM controller** manages the state transitions (Idle, Bank active, Reading, Writing, Precharging, Refresh) based on memory requests and timing constraints. It communicates with the SDRAM chip using signals like reset, clk, addr, data, req, we, ack, valid, and q. Timing diagrams illustrate the sequence of signals for read and write operations, including chaining multiple requests.

### [[System Level Memory]]

- At the **system level**, memory organization involves several key components and concepts.
- A **memory channel** consists of the physical wires on a motherboard that form a data bus and an address/command bus connecting the memory controller to memory chips. The address/command bus is typically unidirectional (controller to memory), carrying address ($a$ bits) and command ($c$ bits) signals. The data bus is bidirectional ($d$ bits), transferring data between memory chips and the controller for read and write operations. Example dimensions are $a=17, c=5, d=64$.
- **DIMMs (Dual In-line Memory Modules)** are the physical memory modules that plug into the memory channels on the motherboard. Each DIMM is a printed circuit board (PCB) with DRAM chips on both sides. Sometimes a DIMM is also referred to as a bank, which can be confusing with the internal banks of a DRAM chip.
- A **rank** is a collection of DRAM chips on a DIMM that are electrically connected such that they operate together to provide the full width of the data bus (e.g., 64 bits) in a single memory cycle. On a rank, each data wire of the memory channel is connected to only one DRAM chip pin, while address/command wires are connected to every DRAM chip.
- A **bank** (within a rank and DRAM chip) is an internally addressable section of the DRAM array that can operate somewhat independently, allowing for parallelism in memory access. Each bank can have its own sense amplifiers. Banks can be further divided into **sub-banks** (a non-standard term for the part of a bank in a single DRAM chip) and **subarrays**, which are rows of **mats**. A mat is a typical 512x512 array of DRAM cells. A memory request might involve activating a single wordline in several mats across different DRAM chips within a rank.
- The **memory pipeline** for a read request has three main stages:

1. Request issued on the address/command bus (~1 ns).
2. Involved DRAM chips in a rank activate their circuits to pick out the required data (~35 ns).
3. The requested data is sent back on the data bus (~5 ns). This is an unbalanced pipeline with a long second stage, so **parallelism** is crucial for efficient data bus utilization. Sources of parallelism include multiple ranks (on the same or different DIMMs), multiple banks within a rank, and the internal organization into sub-banks and mats.

- **Memory access cases** have different latencies depending on the state of the **row buffer** within a bank:
- **Page-hit timing**: The requested cache line is already in the row buffer. Latency is mainly the time to transfer data from the mat to the output pins ($t_{CAS}$). This leverages **spatial locality**.
- **Page-empty timing**: The row buffer is empty, but bitlines are precharged. Latency includes the row activation time ($t_{RCD}$) plus the transfer time.
- **Page-miss timing**: A different row is currently in the row buffer. Latency is the sum of precharge time ($t_{RP}$), row activation time ($t_{RCD}$), and transfer time.
- **High Bandwidth Memory (HBM)** is a type of 3D-stacked DRAM connected using through-silicon vias (TSVs) and microbumps. It connects to the GPU/CPU via an interposer, rather than on-chip, offering much higher bandwidth and lower power consumption through very wide buses.

### [[Memory Scheduler]]

- The **memory scheduler** is a component of the memory controller that manages the flow of memory requests to the DRAM chips.
- When there is an LLC (Last-Level Cache) miss, a read request for a cache line is sent to the memory controller. If a dirty line in the LLC is displaced, a write request for that line is also sent.
- The memory controller typically maintains **read and write queues** to buffer these requests.
- The memory scheduler reorders the requests in these queues based on certain heuristics to improve performance (e.g., by exploiting bank parallelism or prioritizing critical requests).
- The scheduler then selects one or more requests (after considering timing constraints) and moves them into **per-bank command queues**, one for each bank in the memory channel. Once in the command queue, the order of commands for a specific bank is usually maintained (cannot be reordered).
- The head of each per-bank command queue is checked for readiness (satisfying timing constraints).
- A ready command is then selected (e.g., using a round-robin scheme or other policies) and issued to the memory channel using the physical interface (PHY).
- One example scheduling policy is **First Ready, First Come First Served (FR-FCFS)**.
- Memory access scheduler architectures maintain information about each request, such as validity, load/store type, address (row and column), data (for writes), and any additional state needed for the scheduling algorithm.

### [[Virtual Memory and Caches]]

- When a processor needs to access memory, it issues a **virtual address (VA)**. The **memory subsystem**, however, deals with **physical addresses (PA)** that correspond to the actual locations in main memory.
- The **virtual memory subsystem** in the operating system is responsible for performing the **VA to PA translation**. This translation often involves looking up entries in page tables, which may be cached in a Translation Lookaside Buffer (TLB).
- **Caches** are smaller, faster memories that store copies of frequently accessed data from main memory to reduce access latency. When the processor accesses a memory location, the cache is checked first.
- To determine if the requested data is in the cache (a **hit**) or not (a **miss**), the cache performs two key functions:

1. **Indexing**: The address (either VA or PA, or a combination) is used to select a set within the cache where the data might be stored. The index bits of the address determine the set.
2. **Tag matching**: The tag bits from the address are compared with the tags of the data blocks (cache lines) stored in the selected set. If a tag matches and the valid bit is set, it's a cache hit. The tag bits uniquely identify the original memory location of the cache line.

- The interaction between address translation and data caching can be complex. Different organizations exist based on whether the virtual or physical address is used for indexing and tagging:
- **VIVT (Virtual Index, Virtual Tag)**: Virtual address is used for both indexing and tag matching. Allows for faster hit determination as translation is not needed initially, but suffers from aliasing issues (multiple VAs mapping to the same PA).
- **VIPT (Virtual Index, Physical Tag)**: Virtual address is used for indexing, and the physical address (obtained after translation) is used for tag matching. This can have a performance advantage in L1 caches because the index is available before translation. However, tag comparison must wait for TLB lookup.
- **PIVT (Physical Index, Virtual Tag)**: Physical address is used for indexing, and virtual address for tagging. Less common due to the need for translation before cache access.
- **PIPT (Physical Index, Physical Tag)**: Physical address is used for both indexing and tag matching. Avoids aliasing issues but requires address translation before cache lookup, potentially increasing latency. L2 and LLC are often PIPT.
- Several issues need to be considered in the design and management of virtual memory and caches:
- **Flushing of caches on context switch**: When the OS switches between processes, the contents of the cache might belong to the previous process. Flushing (invalidating) the cache or using Process IDs (PIDs) as part of the tag can address this.
- **Aliasing**: Two different VAs mapping to the same PA can cause coherence problems in VIVT caches. **Page coloring** (using set-associative mapping for VM) is a technique to mitigate this.
- **Memory-Mapped I/O (MMIO)**: I/O devices are often accessed through memory addresses. These accesses typically use physical addresses and might bypass caches or have specific coherence requirements.

### [[Load Store Queue]]

- The **Load Store Queue (LSQ)** is a hardware structure in out-of-order processors that buffers load and store instructions after they have been decoded but before they are issued to the memory subsystem.
- The LSQ plays a crucial role in handling **memory dependencies** between instructions. Two memory instructions ($I_1$ and $I_2$) can have dependencies:
- **Dependence through registers**: $I_2$ might use a register that was written by $I_1$.
- **Dependence through memory**: $I_1$ and $I_2$ might access the same memory location.
- The LSQ helps to:
- Maintain program order for memory operations to ensure correctness.
- Detect and resolve data hazards involving memory (RAW - Read After Write, WAR - Write After Read, WAW - Write After Write). **RAW dependencies** (producer-consumer relationship) must be respected. **WAR (anti-dependence)** and **WAW (output dependence)** are **name dependencies** that can be eliminated by register renaming.
- Allow loads to execute out of order (potentially earlier) if there are no preceding unresolved stores to the same address.
- Ensure that stores update memory in the correct order, especially with respect to preceding loads to the same address (store-to-load forwarding). Stores typically wait until their address is resolved and it's safe to update memory.
- The LSQ typically operates by:
- When a load instruction enters the LSQ, it checks all preceding stores in the queue.
- If a store to the same address is found, the load can terminate and forward the value from the store.
- If a preceding store has an unresolved address, the load might need to wait.
- If no such store is found, the load can be sent to the data cache (D$).
- When a store instruction enters the LSQ, it checks all subsequent stores in the queue for WAW hazards (terminate if another store to the same address is found later). It also checks for subsequent loads to the same address for potential store-to-load forwarding.
- For efficient implementation, the LSQ can be organized as two separate, circular queues: a **load queue** and a **store queue**.
- At each cycle, the LSQ can perform several operations, including computing effective addresses, finding queue locations of interest, enqueuing and dequeuing operations, resolving memory operations upon address calculation, and handling queue size limits.

### [[Cache Organization]]

- A cache is organized into multiple **cache lines** (also called blocks), which are fixed-size units of data transfer between the cache and main memory.
- The cache is divided into **sets**, and each set can hold one or more cache lines (depending on the **associativity** of the cache).
- A **direct-mapped cache** has one cache line per set (associativity = 1).
- An **$A$-way set-associative cache** has $A$ cache lines per set.
- A **fully-associative cache** has only one set and can hold any cache line (associativity = number of cache lines).
- A cache address is typically divided into three fields:
- **Tag**: Identifies the specific memory block stored in the cache line.
- **Index**: Selects the set in the cache where the block might reside. The number of sets $S = C / (A \times B)$, where $C$ is the cache capacity and $B$ is the block size.
- **Offset**: Selects the specific byte (or word) within the cache line. If the block size is $B$, then $\log_2(B)$ bits are used for the offset.
- The cache structure typically includes a **data array** to store the actual data and a **tag array** to store the tags and status bits (like valid and dirty bits) for each cache line. **Comparators** are used to compare the tag from the CPU request with the tags in the selected set to detect a hit or miss.
- **Content Addressable Memory (CAM)** cells can be used in tag arrays for faster parallel tag comparison, especially in highly associative caches. A CAM cell checks if its stored value matches an input key.
- **Cache Line Replacement Policies** are needed for set-associative caches to decide which cache line to evict when a new block needs to be brought into a full set. Common policies include Least Recently Used (LRU) and Most Recently Used (MRU). Implementing these can be complex, especially with higher associativity. For a 2-way set-associative cache, a single bit per set can track MRU or LRU.
- **Advanced Cache Design Choices** can improve performance:
- **Pipelined Cache**: If the best-case cache access latency is multiple processor cycles, pipelining can improve throughput by adding pipeline registers between cache stages (e.g., tag access, data access, tag comparison, data selection). Read and write operations can be divided into multiple pipeline stages.

  

## [[Multiprocessor Issues]], [[Memory Consistency]], [[Cache Coherence]], and [[MESI Protocol]]

### I. Multiprocessor Issues

The advent of multicore processors introduces a new set of challenges in computer architecture. In a system with multiple processing cores, each capable of executing instructions and accessing a shared memory space, ensuring correct and efficient operation becomes significantly more complex.

**Shared Memory Parallelism:** Multiprocessor systems enable shared-memory parallelism, where multiple processor cores can read and write to a single shared address space. This paradigm allows for concurrent execution of program threads, potentially leading to significant performance gains.

**The Challenge of Correctness:** A fundamental question in shared-memory systems is the definition of correctness. With multiple actors (processor cores, DMA engines, external devices) accessing caches and memory, maintaining a consistent view of data becomes crucial. The core issues that arise in this context are **memory consistency** and **cache coherence**.

**Need for Management:** Subsystems like memory and external devices, which are not necessarily on the processor itself, need to be allocated and shared correctly among the multiple cores. This necessitates mechanisms to manage access to shared resources and maintain a coherent state across the system.

### II. [[Memory Consistency]]

**Definition:** Memory consistency is a precise, architecturally visible definition of shared memory correctness. It provides a set of rules that govern how memory operations (loads and stores) are executed and how they act upon the shared memory. A consistency model defines what constitutes a correct execution of a multithreaded program by specifying the permissible orderings of memory operations across different cores. It allows for many correct executions while disallowing incorrect ones.

**Consistency vs. Coherence:** It's important to distinguish between memory consistency and cache coherence. Consistency is the architectural contract that the system must uphold, defining the semantics of memory operations as observed by the programmer. Coherence, on the other hand, is a microarchitectural mechanism that aims to support a chosen consistency model. It deals with ensuring that cached copies of shared data remain up-to-date when one processor modifies its copy. Incoherence arises when a change made by one core to a shared value in its cache is not made visible to other cores that might also be caching the same value.

**Baseline System Model:** To understand memory consistency, it's useful to consider a baseline system model consisting of multiple single-threaded cores, each with a private write-back (WB), physical index, physical tag (PIPT) data cache (D$), sharing a last-level cache (LLC) connected by an interconnection network. All cores can perform loads and stores to all physical addresses.

**Pipeline-Coherence Interface:** Processor cores interact with the coherence protocol through a coherence interface, typically with methods for read requests and write requests. A coherence protocol can be consistency-agnostic (writes are made visible synchronously before returning) or consistency-directed (writes can return before being visible to all, propagated asynchronously).

**Consistency-Agnostic Coherence Invariants:** Consistency-agnostic protocols often rely on coherence invariants to ensure correctness:

- **Single-Writer, Multiple-Read (SWMR) Invariant:** For any memory location at any given time, there is either a single core that can write to it (and also read it) or multiple cores that can only read it.
- **Data-Value Invariant:** The value of a memory location at the start of an epoch (a period between writes) is the same as the value at the end of the last read-write epoch.

#### A. Sequential Consistency (SC)

**Definition:** Sequential Consistency (SC) is a strong memory consistency model.

- A single core is sequential if the result of its execution is the same as if its operations were executed in the order specified by the program.
- A multiprocessor is sequentially consistent if the result of any execution is the same as if the operations of all cores were executed in some sequential order, and the operations of each individual core appear in this global sequence in the order specified by its program. This implies a total order of all memory operations, called **memory order** ($<_{m}$), which respects each core's program order ($<^{c}_{p}$).

**SC Formalism:** SC execution requires that all cores insert their loads ($L(a)$) and stores ($S(a)$) into the global memory order, respecting their local program order, regardless of the memory address. Every load must retrieve the value of the last store to the same address that precedes it in the memory order. An SC implementation must only permit SC executions (safety) and ensure that a store will eventually become visible to a load trying to read that location (liveness).

**Basic SC Implementation using Cache Coherence:** A basic approach to implementing SC leverages cache coherence to maintain the SWMR invariant. L1 caches can be in two states: Modified (M) for exclusive read/write access, and Shared (S) for read-only access by one or more cores. Coherence requests like GetM (to obtain a block in M state) and GetS (to obtain a block in S state) are used.

#### B. Total Store Order (TSO) Consistency Model

**Definition:** Total Store Order (TSO) is a more relaxed (weaker) consistency model than SC. It was introduced to support write buffers for performance reasons. While a write buffer (WB) with load bypassing is architecturally invisible in a single-core processor, it becomes visible in a multicore scenario.

**The Problem with Write Buffers and SC:** Consider two cores (C1 and C2), each with a single-entry write buffer. If C1 executes a store (S1: x = NEW) and buffers the new value, and C2 similarly executes a store (S2: y = NEW), followed by each core executing a load (L1: r1 = y and L2: r2 = x) before their write buffers update memory, both loads might read the old values (e.g., 0). This outcome violates SC because there is no sequential interleaving of operations from both cores that could produce this result; the stores should appear to complete before the subsequent loads observe the old values.

**TSO Characteristics:** TSO allows the use of a simple FIFO write buffer at each core and permits the non-SC execution described above. In TSO, all writes from a single processor are performed in program order (hence, "Total Store Order"), but a processor can observe its own writes before they are visible to other processors, and loads can bypass pending writes in the write buffer (load bypassing).

**TSO Formalism:** Similar to SC, TSO has a formalism involving program order ($<^{c}_{p}$) and memory order ($<_{m}$) for loads, stores ($S(a)$), and atomic read-modify-write operations ($RMW(a)$). TSO also introduces the concept of a **FENCE** instruction, which acts as a synchronization point, ensuring that all memory operations preceding the fence in program order are placed in the memory order before any operations following the fence.

**Relaxed Consistency Models:** TSO is an example of a consistency model that relaxes some of the requirements of SC to enable higher performance through microarchitectural optimizations like write buffers. Different consistency models offer varying degrees of relaxation, leading to different trade-offs in programmability and performance. A model Y is strictly more relaxed than a model X if all X executions are also Y executions, but not vice versa.

### III. [[Cache Coherence]]

**Definition:** Cache coherence is a microarchitectural mechanism that ensures that multiple caches in a shared-memory system maintain a consistent view of the same memory locations. When one processor modifies a data item that is also cached by other processors, the coherence mechanism must ensure that these other processors eventually see the updated value. Without coherence, different processors could operate on stale or incoherent data, leading to incorrect program behavior.

**Coherence Invariants:** Coherence protocols aim to maintain the SWMR and Data-Value invariants to ensure a degree of consistency, even if the overall memory consistency model is weaker than SC.

**Coherence Controller:** The mechanism used to achieve cache coherence is typically a **coherence controller**, which is a Mealy finite-state machine (FSM) associated with each storage structure (i.e., each cache and the LLC/memory). Logically, it can be viewed as a collection of identical but independent FSMs, one for each memory block or cache line. These controllers exchange messages to ensure that the coherence invariants are always maintained. The **coherence protocol** specifies the interactions between these FSMs.

**Simple Coherence Protocol Example:** A basic protocol can have two stable cache line states: Invalid (I) and Valid (V), and two stable memory block states: I (all caches in I) and V (one cache in V). A transient cache state, such as IVD (Invalid to Valid, waiting for Data), can also exist.

**Coherence Protocol Design Space:** Several boolean characteristics define the state of a cache line in more advanced protocols:

- **Validity:** Whether the cache line holds the most up-to-date value for the memory block.
- **Dirtiness:** Whether the cached value has been modified and differs from the value in the LLC/memory, making the cache responsible for updating the memory.
- **Exclusivity:** Whether this is the only privately cached copy of the memory block in the system.
- **Ownership:** Which controller (cache or memory) is responsible for responding to coherence requests for the block.

**Common Transactions:** Coherence protocols involve various transactions, such as read requests (for shared or exclusive access), write requests, data responses, and acknowledgments.

**Protocol Design Options:** The two main design options for coherence protocols are:

#### A. Snooping Protocols

- In a snooping protocol, every cache controller monitors (snoops) all coherence requests broadcast on the interconnection network (typically a shared bus).
- All coherence controllers observe these requests in the same order and collectively perform the necessary actions to maintain coherence ("do the right thing").
- The ordered broadcast network ensures a total order of all coherence requests, simplifying the implementation of strong consistency models like SC and TSO.
- Snooping protocols are generally simpler to specify and implement but can face scalability challenges due to the broadcast nature and the need for a totally ordered network, making them less suitable for large-scale multicore systems beyond a single chip.

#### B. Directory Protocols

- In a directory protocol, a centralized **directory** (typically located at the memory controller) maintains a global view of the coherence state of each block in the LLC/memory.
- When a cache controller needs a block, it sends a unicast request to the directory, which then determines the appropriate action, such as responding with the data or forwarding the request to the current owner of the block.
- The interconnection network enforces point-to-point ordering of messages between the requester and the directory, and the directory acts as the point of serialization for coherence transactions.
- Conflicting requests are processed in per-block order at the directory, not necessarily in a total global order.
- Directory protocols are inherently more scalable than snooping protocols as they avoid broadcasts, but they introduce the complexity of managing the directory and ensuring it doesn't become a performance bottleneck. Careful design is needed to prevent deadlocks during message passing.

**Invalidate vs. Update:** Another design choice within coherence protocols is whether to invalidate or update remote caches when a write occurs:

- **Invalidate:** When a core writes to a block, it sends invalidation messages to all other caches holding a copy, forcing them to mark their copies as invalid. Subsequent reads by these cores will then fetch the updated value from memory or the writing core. This is the more common approach as it avoids the overhead of updating potentially unused copies.
- **Update:** When a core writes to a block, it sends update messages to all other caches holding a copy, providing them with the new value. This can reduce the latency of subsequent reads but introduces overhead even if the updated value is not immediately needed.

### IV. [[MESI Protocol]]

The MESI protocol is a widely used **snooping-based** cache coherence protocol. The name comes from the four states that a cache line can be in:

- **Modified (M):** The cache line holds the most recent, exclusive, and dirty copy of the data. It has been modified and is not present in main memory in its current form. The cache is responsible for writing it back to memory when it is evicted. This state satisfies Validity, Dirtiness, Exclusivity, and Ownership (implicitly).
- **Exclusive (E):** The cache line holds the only valid copy of the data, and it is clean (not modified). It is consistent with main memory. The cache has exclusive access and can transition to the Modified state without a bus transaction if it writes to the line. This state satisfies Validity and Exclusivity.
- **Shared (S):** The cache line holds a valid copy of the data, which may also be present in other caches. The data is clean and consistent with main memory. Multiple caches can be in the Shared state.
- **Invalid (I):** The cache line does not hold a valid copy of the data. Any access to this line will result in a cache miss, triggering a coherence transaction to fetch the data.

**Snooping MESI Operation:** In a snooping MESI protocol, all caches on the bus snoop on all bus transactions. When a core performs a read or write that results in a cache miss, the cache controller issues a request on the bus. Other caches monitor this request and respond based on the state of the requested cache line in their own caches. Main memory also participates in responding to requests if no cache has the most up-to-date copy.

**Cache Controller FSM (Snooping MESI):** Each cache has a controller that manages the state transitions of its cache lines based on local processor requests (reads, writes) and bus snoop responses to requests from other caches. For example, a read miss for a block in the Invalid state will cause a request on the bus. If another cache has the block in Modified state, it will provide the data and transition to Shared (or Owned in MOESI). Main memory will provide the data if no cache has it in M or E state, and the requesting cache will transition to Shared (or Exclusive if it was a read for exclusive access). A write to a block in Shared state requires first obtaining exclusive ownership, typically through an invalidation bus transaction that forces all other shared copies to Invalid.

**Memory Controller (Snooping MESI):** The memory controller in a snooping system typically snoops on the bus as well. It generally provides data for read misses if no cache has the block in M or E state. It also gets updated data when a cache writes back a Modified block.

**Directory MESI:** The MESI protocol can also be implemented using a directory-based approach. In this case, the directory at the memory controller maintains the coherence state of each memory block and a list of which caches (if any) have a copy. When a cache needs a block, it requests it from the directory. The directory then sends messages to the appropriate caches (e.g., to invalidate a copy or to forward the data) and responds to the requesting cache. The states (Modified, Exclusive, Shared, Invalid) have similar meanings but the transitions and communication paths differ from the snooping version.

**Advantages and Disadvantages:**

- **Snooping MESI:** Simpler to implement for small-scale systems with a shared bus, easier to reason about due to the total order of requests. However, it doesn't scale well to larger systems due to bus contention and the overhead of snooping.
- **Directory MESI:** More scalable as it uses point-to-point messages and avoids broadcasts. However, it is more complex to implement and manage the directory, and the latency of coherence transactions might be higher due to the indirection through the directory.
