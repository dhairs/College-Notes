## L1 Instruction Memory System

Fetches instruction from the Instruction cache (I$) and delivers the instruction stream to the instruction decode unit. 

It includes:
- a 64 KiB ([[Special Notation#Kibibyte (KiB)|Kibibyte]]), 4 way Set Associative L1 I\$ with 64B lines
- a fully-associative L1 ITLB with native support for 4 KiB, 16 KiB, 64 KiB, and 2 MiB page sizes
- A 1536-entry 4-way **skewed associative** L0 **Macro-Op** (MOP) cache, which contains decoded and optimized instructions for higher performance. 
- A dynamic branch predictor: [[Branch Prediction#Tagged Hybrid Predictors|TAGe]], branch target buffers, return address stacks, etc.

| ![[Neoverse V2 Decode and Blocks.png]]                              |
| ------------------------------------------------------------------- |
| https://www.scs.stanford.edu/~zyedidia/docs/arm/neoverse_v2_trm.pdf |

## Macro-Ops (MOPs) and Micro-Ops (µops)

**Macro-Op (MOP)**: An instruction held in a format described by the ISA. Can be slight differences, but basically the same. This is independent of the µ-architecture.

**Micro-Op (µop)**: An internal processor specific encoding of the operations used to control execution resources. This can vary widely between different implementations of the same ISA.

The correspondence between MOPs and µops used by a processor may be 1:1, 1:N, or N:1: A single MOP can be **cracked/split** into one or more internal µops, or multiple MOPs can be **fused** into a single µop.

## Pre-Decoding


| ![[Pasted image 20250312102658.png]] |
| ------------------------------------ |
|                                      |
