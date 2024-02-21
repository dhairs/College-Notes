## Instruction Processing

Recall how we define [[Instruction Set Architectures]].

1. Fetch 32-bit instruction word (IW) from memory location pointed to by program counter (PC)
2. Decode the instruction word
	1. IW = (**operation**, *operands*, ==result== locations)
	2. Read operands from registers
3. Execute arithmetic/logic for operation
4. Access memory *if needed*
	1. Either a load or a store
5. Write ==results== back to registers *if needed*
6. Update [[AArch64 (ARM) State and Programming Model#^6298e8|Program Counter]] (PC)

## Sources and Destinations

The generic form of an instruction is IW = (**operation**, *operands*, ==result== locations)

Operands can be:
- A constant value; the contents of a register; the contents of one or more memory cells (R-Values). 

R