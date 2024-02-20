## About

The ARM Architecture describes the behavior of an **abstract machine**.

The programmer visible part should **seem** like the implementation is sequential, and it should always be correct. The execution time doesn't count in this description.

## Execution States and Profiles

### Execution States

**AArch64**: [[Operations on Representations#Word Size|Word Size]] of 64. Addresses held in 64 bit registers. Supports the ==A64== instruction set. Instructions are still 32 bits wide.

**AArch32**: [[Operations on Representations#Word Size|Word Size]] of 32. Addresses held in 32 bit registers. Supports the ==A32== and ==T32== instruction sets. Instructions are 32 bits wide. (not discussed in this class)

### Execution Profiles

**A-profile (Application)**: Supports virtual memory; supports A64, T32, A32 instruction sets

**R-profile (Real-Time)**: Supports protected memory; supports A32 and T32 instruction sets

**M-profile (Microcontroller)**: implements a programming model designed for low latency interrupt processing; supports a variant of the T32 instruction set.

## Exception Levels (EL)

These are similar to the privilege levels we talk about in [[Instruction Set Architectures]].

ARM defines **four exception levels**: EL0, EL1, EL2, and EL3.
- EL3 is the highest exception level, EL0 is the lowest
	- Meaning EL3 is the highest privilege possible
- Unprivileged execution is any execution that happens at EL0

Any implementation of the architecture must include at **least** EL0 and EL1, EL2 and EL3 are optional.

## ARM Architecture Characteristics

- A large uniform register file
	- Remember we talk about [[Instruction Set Architectures#The von Neumann Architecture|von Neumann Architectures]] having small, quickly accessible registers on the processor to hold instructions and memory.
- A load/store architecture
	- Data processing operations only operate on register contents, not directly on memory contents
	- Loading is getting it into the register, then the value is edited, and then it is stored back into memory
- 