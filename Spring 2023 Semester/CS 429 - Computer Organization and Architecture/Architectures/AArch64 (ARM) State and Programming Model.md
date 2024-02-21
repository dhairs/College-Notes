## About

The ARM Architecture describes the behavior of an **abstract machine**.

The programmer visible part should **seem** like the implementation is sequential, and it should always be correct. The execution time doesn't count in this description.

## ARM Architecture Characteristics

- A large uniform register file
	- Remember we talk about [[Instruction Set Architectures#The von Neumann Architecture|von Neumann Architectures]] having small, quickly accessible registers on the processor to hold instructions and memory.
- A load/store architecture
	- Data processing operations only operate on register contents, not directly on memory contents
	- Loading is getting it into the register, then the value is edited, and then it is stored back into memory
- Simple addressing modes
	- With all load/store addresses determined from register contents and instruction fields only

## Exception Levels (EL)

These are similar to the privilege levels we talk about in [[Instruction Set Architectures]].

ARM defines **four exception levels**: EL0, EL1, EL2, and EL3.
- EL3 is the highest exception level, EL0 is the lowest
	- Meaning EL3 is the highest privilege possible
- Unprivileged execution is any execution that happens at EL0

Any implementation of the architecture must include at **least** EL0 and EL1, EL2 and EL3 are optional.

## Execution States and Profiles

### Execution States

**AArch64**: [[Operations on Representations#Word Size|Word Size]] of 64. Addresses held in 64 bit registers. Supports the ==A64== instruction set. Instructions are still 32 bits wide.

**AArch32**: [[Operations on Representations#Word Size|Word Size]] of 32. Addresses held in 32 bit registers. Supports the ==A32== and ==T32== instruction sets. Instructions are 32 bits wide. (not discussed in this class)

### Execution Profiles

**A-profile (Application)**: Supports virtual memory; supports A64, T32, A32 instruction sets

**R-profile (Real-Time)**: Supports protected memory; supports A32 and T32 instruction sets

**M-profile (Microcontroller)**: implements a programming model designed for low latency interrupt processing; supports a variant of the T32 instruction set.

## AArch64 Execution State

- Registers **R0-R30**
	- 31 64-bit wide general purpose registers (GPRs)
	- Access as 64 bit registers using names X0-X30
	- Access as 32 bit registers using names W0-W30
	- X30 GPR **reserved** for use as a procedure call link register (a what?)
	- The Zero Register (ZR) is a **pseudo-register** that is encoded as X31. Reading it provides you the bits 0x0. Writes to it aren't performed.
- Stack pointer **SP**
	- 64 bit dedicated Stack Pointer register
	- Least significant 32 bits can be accessed as WSP (Remember W just denotes the 32-bit variant)
	- SP must be aligned to a 16-byte boundary
- Program Counter **PC**
	- Tells the machine what instruction it is processing 
	- 64 bit program counter holding the address of the current instruction
	- Software can't write directly to the PC
		- The default update rule is `PC <- PC + 4` (because instructions are 4 bytes wide), this is called **sequential access**
		- Any update to any other value happens only as the side effect of a branch/call/return instruction (we need to jump to another place in memory)
- Process State **PSTATE**
	- An abstraction of process state information
	- At EL0, there are only 4 flags we are able to access:
		- **N**: Negative condition flag
		- **Z**: Zero condition flag
		- **C**: (Unsigned) Carry condition flag
		- **V**: (Signed) oVerflow condition flag
		- These flags turn on whenever the instruction just performed had any of the above occur.

## AArch64 Memory Model

Address calculations are performed using 64 bit registers (addresses are always 64 bits long, so this is natural)

Two memory types:
1. **Normal**: used for most reads and writes
2. **Device**: Memory locations where an access to the location can cause side-effects, or where the value returned for a load can vary depending on the number of loads performed
	1. Typically used for memory mapped peripherals and similar locations
	2. Think of ports on a computer — its an effective way to communicate between them
	3. **Memory Mapped I/O**

Alignment
- Instructions must be 4-byte aligned
	- Misalignment results in a fault
- Data alignment rules are complex, but you *can* do unaligned operations
	- Unaligned access is supported, but it is much slower
- Endianness
	- A64 instructions have a fixed length of 32 bits and are always little-endian
	- Data endianness of normal memory is configurable at EL1+
	- All memory mapped peripherals must be little endian