## What is Main Memory

Main Memory, or Primary Memory, is memory that is used to store the data and programs or instructions during computer operation. It is _usually_ either RAM (random access memory) or ROM (read-only memory).

## Dynamic RAM (DRAM)

DRAM cells have a structure of 1 transistor and 1 capacitor. In DRAM, the two states are signified by the presence (or absence) of trapped charge on the capacitor.

The [[Bits and Bit Technologies#^e5350b|MOSFET]] is the control when storing charge when writing, and also senses the presence of charge in reading. However, these capacitors discharge over time and require periodic refreshes to maintain state.

For this reason, the DRAM cell is sensitive to noise and leakage, and is not persistent, but can handle **many many** read and write cycles without breaking.

## Single In-line Memory Modules (SIMMs) and Dual In-line Memory Modules (DIMMs)

Typical computers have 2-4 DIMMs on the motherboard.

A **Rank** is the chips we have on a ram stick that sends data at a time. So, if we have a 2 sided RAM stick with 8 chips each on each side, we have a multi-rank RAM with 2 ranks. This basically defines the capacity of memory we have.

### What's inside of a chip

#### DRAM

Typically described by a pair of numbers ($d\times w$). E.g., $54\text{M}\times 16$, $8\text{M}\times 8$, etc.

Such a chip stores $d\cdot w$ bits of data, organized as $d$ **supercells**, also called **cells** or **words**, each containing $w$ bits. Each access to a supercell results in _all_ its bits being read.

The $d$ supercells for a rectangular array in turn consist of $r$ rows and $c$ columns, such that $r\cdot c=d$. These access are controlled by a block called the **memory controller**, typically in the processor chip.

Memory is typically in powers of 2 (because, you know, we like [[Bits and Bit Technologies|binary stuff]]), so instead of Megabytes (M), we actually have [[Special Notation#Mebibyte (MiB|Mebibytes (Mi)]].

Each chip with an 8-bit output is wired to the 64-bit data bus. The multiple chips service the data bus in parallel.

##### Internal Row Buffer and Spatial Proximity

The process of reading involves first reading an entire row and putting it into a row buffer, and this is very slow.

If we expect spatial locality, then the next set of bytes may be needed from the same row, and so in that case:

- We shouldn't discard that row from the row buffer because it contains many neighboring supercells
- If the memory controller can identify the next requirement already exists, then we can save reading the entire row again

##### Banks

The chips are divided up into banks. Operations on the banks are pipelined to keep the data bus activity constant for a higher throughput. So, each memory module is divided up into chips, which are each divided up into banks.

These banks in each chip are accessed in parallel through the same control and data bus lines. So every bit of the 64 bits we request is going to come from a different bank if we have 8 chips with 8 banks each.

##### Error Detection and Correction

DRAMs are usually quite error prone, so we need a way to detect and correct errors. Typically, we need some additional bits along with data to detect and correct errors, these are added on using additional ECC DIMMs which could be X8.

**Hamming codes** are one of the most common ways to do this, where we store the minimum distance between two code words, with a minimum distance of 3.

#### Hamming Codes

- Parity bit p1 finds the parity for data bits d1, d2, and d4
- Parity bit p2 finds the parity for data bits d1, d2, and d4
- Parity bit p4 finds the parity bits for d2, d3, and d4

The data bits d1, d2, d3, d4, and the parity bits p1, p2 and p4 are transferred to the receiver. At the receiver, the parity bits are kept aside and the parity bits of the received data bits are recomputed. If the recomputed parity bits and received parity bits are mismatching, we got an error.
