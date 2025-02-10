## Terminology

**Memory Channel**: Wires on a motherboard making up a data bus and an address/command bus.
- The address/command bus is a unidirectional bus that carries $a$ bits of address and $c$ bits of command from the memory controller to the memory chips
- The data bus is bidirectional and carries $d$ bits of data from the memory chips to the memory controller for a read request, and vice versa for a write.
- Assume that $a=17,c=5,d=64$

**DIMM**: The memory modules that plug into a memory channel.
- Each DIMM is a printed circuit board (PCB) with memory chips on the front and back.
- Each DIMM is also referred to as a **bank**.

**Rank**: A collection of DRAM chips on a DIMM that all work together to keep the 64-bit data bus busy in a cycle.
- A single data wire on the memory channel is only connected to one DRAM chip pin on a rank at a time
- An address/command wire on the memory channel is connected to every DRAM chip on every rank on the channel.

**Bank**: A collection of chips inside of a rank.

## Memory Pipeline

### Immediate Issue with Pipelining Memory

1. Request Issues on address/command bus (~1ns)
2. Involve DRAM chips in a rank activate their circuits to pick out the required data (~35ns)
3. The requested data is sent back on the data bus (~5ns)

This leads to a three staged unbalanced pipeline. One stage is exceedingly large compared to the others.

To fully utilize the data bus, multiple requests must be working on the second stage in parallel.

### Sources of Parallelism

We have multiple ranks within a channel, possibly on different DIMMs. We also have multiple banks within a rank.

Each bank is further composed of into **sub-banks**, the part of a bank resident in a single DRAM chip, this is not a standard term. The banks typically share a bus that moves data between the banks and the I/O pins.

A bank is partitioned into multiple **subarrays**, which is a row of mats.

Each subarray is partitioned into a number of **mats**. A mat is typically 512 rows and 512 columns of DRAM cells.

A data request involves several mats on several DRAM chips. It activates a single wordline in each. mat, with all the DRAM cells in that row placing their data on the bitlines.

### M