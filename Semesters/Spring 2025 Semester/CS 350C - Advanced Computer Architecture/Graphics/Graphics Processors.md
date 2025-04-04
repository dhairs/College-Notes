## GPUs

Graphics processing units use their own microarchitecture to orchestrate and perform operations over data. There are very specific ways to use these processors, since they are highly parallel. 

The most common library for GPUs is NVIDIA's [[CUDA]].

## The Graphics Processing Cluster

## Structure of a Streaming Multiprocessor (SM)

![[Streaming Multiprocessor.png|300]]


| Type of Memory    | Functionality                                                                                                                                    |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Instruction cache | Similar to an i-cache                                                                                                                            |
| L1 cache          | Stores regular data                                                                                                                              |
| Texture cache     | Stores texture information                                                                                                                       |
| Constant cache    | Stores constants                                                                                                                                 |
| Shared memory     | A shared memory that all the threads in<br>the SM can access. Typically, the<br>__shared__ identifier is used to store<br>arrays in this region. |
## Warps

On a given unit, we can process a TON of threads at once: 

$$6\text{ GPC} \times 7 \frac{\text{TPC}}{\text{GPC}}\times 2\frac{\text{SM}}{\text{TPC}}\times_{4} \frac{\text{PB}}{\text{SM}}\times 16 \frac{\text{threads}}{\text{PB}}=5367 \text{ threads}.$$

We can't afford to put a [[AArch64 (ARM) State and Programming Model#^6298e8|Program Counter]] (PC) on every thread, that would take up too much memory bandwidth and require a rework of memory systems. Instead, we can create a **warp**: 
- Groups of 32 threads
- Give them all the same PC
- Make them execute **in lockstep** — this is important, if one thread stalls, the others do, too.

This is analogous to a vector instruction with $VL=32,16$ hardware lanes and $\text{chime}=2$ clock cycles.


## Code with Conditional Branches

