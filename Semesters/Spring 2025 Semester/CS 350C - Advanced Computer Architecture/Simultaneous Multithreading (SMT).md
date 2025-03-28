## Definition

Technique that permits multiple independent threads to issue multiple instructions to a superscalar processor's functional units in a single cycle.

Traditional processors suffer from two types of waste:
- **Horizontal Waste**: Empty issue slots in a non-idle cycle
- **Vertical Waste**: Completely idle cycles

The **key innovation** is that SMT allows different threads to simultaneously share processor resources.

## Performance

In Tullsen, et al. 1996, they evaluated three SMT models:
- **Full Simultaneous Issue**: all threads compete for all issue slots. This was highest performance but also the most complex.
- **Single/Dual/Four Issue**: limited per-thread issue bandwidth. This had a simpler hardware implementation.
- **Limited Connection**: Each hardware context connects to specific functional units. This was the simplest, but also the slowest.

SMT is able to achieve higher throughput than other alternatives, including the simple models.

## Architectural Modifications

- Multiple program counters
- Per-thread return stacks for branch prediction
- Per-thread instruction retirement and trap mechanisms
- Thread IDs in branch target buffer entries
- Large register file (most significant change)
	- Requires pipelined access, extra cycles

Critical Innovation: **ICOUNT Fetch policy**:
- **ICOUNT**: Prioritize threads with fewest instructions in decode, rename, and queues
- 23% gain over round-robin thread selection
- Significantly reduced instruction queue congestion
- Dynamically favors threads using resources efficiently

## Fetch Partitioning Strategies

## Key Technical Challenges

Instruction fetch:
- Thread selection policies: ICOUNT performance improvement up to 37% vs. round-robin

Register File Design:
- Challenges:
	- Must support logical registers for all threads
	- Additional physical registers for renaming
	- Access time becomes critical with large register files
- Solutions:
	- Pipeline register access (multi-cycle read/write)
	- Optimize thread count based on physical register count
	- For 200 physical registers, 4 threads was optimal

Cache Hierarchy:
- Private vs. Shared Caches:
	- Shared caches: Better for few threads
	- Private caches: Better for many threads
- Best configuration:
	- Private instruction caches
	- Shared data cache
	- This balances isolation and efficient sharing

Branch Prediction:
- Challenges:
	- Multiple threads compete for branch prediction resources
	- Misprediction rates increase with thread count
-  Observations:
	- SMT is less sensitive to branch mispredictions
	- Perfect branch prediction: 25% improvement on 1 thread vs 9% improvement on 8 threads
	- SMT Reduces wrong-path instructions from 16% to 9%.

## Commercial Implemented

### Intel Hyperthreading

First appearance: Pentium 4 (Northwood) in 2002. Uses a 2-way SMT (two logical processors per core). Used duplicated architectural state registers, shared execution resources, caches, and TLBs. Some resources statically partitioned. 

Currently enabled in all modern Intel CPUs (up to 2-way SMT).


### AMD SMT

Introduced in the Zen Architecture in 2017. Uses a 2-way SMT (similar to Intel's). Balanced resource sharing and efficient instruction scheduling.

Currently enabled in Ryzen, EPYC, and Threadripper products.


## Modern SMT Considerations

### Power and Efficiency

Advantages:
- Improves performance/watt by better utilizing existing resources
- Higher throughput without proportional power increase

Challenges:
- Dynamic power increases from more active transistors
- Complex power management is required

Solutions: 
- Power-aware thread scheduling
- Dynamic resource partitioning

### Security

Vulnerabilities:
- Side-channel attacks (e.g., Spectre/Meltdown variants)
- Resource sharing enables cross-thread information leakage

Mitigations:
- OS-level scheduling constraints
- Hardware partitioning of critical resources
- Option to disable SMT for security-critical applications

### OS Scheduling

Thread placement matters for performance

Modern OSes are SMT-aware:
- Linux: CPU affinity, thread grouping
- WIndows: logical processor groups
- macOS: thread affinity APIs

Some workloads benefit from disabling SMT and using physical cores only.

## Key Takeaways

SMT significantly improves processor resource utilization with modest hardware changes. The register file is the most challenging resource to scale with SMT. Intelligent fetch policies like ICOUNT provide substantial performance improvements. 

Commercial implementations usually use 2-way SMT for clients, and 8-way for servers. SMT complements multicore designs, improving both throughput and utilization. 

Best cache organization: Private instruction caches with shared data caches. 

Fetch throughput remains a primary bottleneck.
