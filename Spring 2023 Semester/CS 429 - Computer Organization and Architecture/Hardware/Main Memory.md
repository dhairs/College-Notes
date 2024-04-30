## Dynamic Ram (DRAM)

DRAM cells have a structure of 1 transistor and 1 capacitor. In DRAM, the two states are signified by the presence (or absence) of trapped charge on the capacitor.

The [[Bits and Bit Technologies#^e5350b|MOSFET]] is the control when storing charge when writing, and also senses the presence of charge in reading. However, these capacitors discharge over time and require periodic refreshes to maintain state.

For this reason, the DRAM cell is sensitive to noise and leakage, and is not persistent, but can handle **many many** read and write cycles without breaking.

## Single In-line Memory Modules (SIMMs) and Dual In-line Memory Modules (DIMMs)

Typical computers have 2-4 DIMMs on the motherboard.

A **Rank** is the chips we have on a ram stick that sends data at a time. So, if we have a 2 sided RAM stick with 8 chips each on each side, we have a multi-rank RAM with 2 ranks. This basically defines the capacity of memory we have.

### What's inside of a chip
##### DRAM
Typically described by a pair of umbers ($d\times w$). E.g., $54\text{M}\times 16$, $8\text{M}\times 8$, etc.

Such a chip stores $d\cdot w$ bits of data, organized as $d$ **supercells**, also called **cells** or **words**, each containing $w$ bits. Each access to a supercell results in *all* its bits being read.

The $d$ supercells for a rectangular array in turn consist of $r$ rows and $c$ columns, such that $r\cdot c=d$. These access are controlled by a block called the **memory controller**, typically in the processor chip. 

Memory is typically in powers of 2 (because, you know, we like [[Bits and Bit Technologies|binary stuff]]), so instead of Megabytes (M), we actually have Mebibytes (Mi). 