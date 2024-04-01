![[Specifying Operands and Results#Instruction Processing]]

## Architectural Status

Architectural Status is a simplified view of machine health

There are four architectural status codes:
- `STAT_AOK`: **Normal**, code is running
- `STAT_HLT`: **Normal**, code has exited normally
- `STAT_INS`: **Error**, reported by instruction memory
- `STAT_ADR`: **Error**, reported by data memory

There will be an additional micro architectural status when getting to the pipelined implementation.

## Extracting Instructions from Bit Fields

- Extract opcode from the top 11 bits.
	- Use the `itable` to lookup the command 
- Register the operands
- Get immediate operands
- Shift a certain amount
- Condition

## Building Block: [[AArch64 (ARM) State and Programming Model#^6298e8|Program Counter]]

- This is a 64-bit **clocked-register** (edge-triggered D flip-flop) with input side labeled `next_PC[63:0]` and output side labeled `current_PC[63:0]`

