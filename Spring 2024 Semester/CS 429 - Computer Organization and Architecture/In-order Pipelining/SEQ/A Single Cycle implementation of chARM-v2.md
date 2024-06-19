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

## Building Blocks

### [[AArch64 (ARM) State and Programming Model#^6298e8|Program Counter]]

- This is a 64-bit **clocked-register** (edge-triggered D flip-flop) with input side labeled `next_PC[63:0]` and output side labeled `current_PC[63:0]`
- It drives all the combinational logic downstream from it to perform the actions needed to execute an instruction
- The three possible `next_PC` values are:
	- `seq_succ = current_PC + 4` (most instructions)
	- `branch_target = current_PC + branch_offset` (For B, BL, and B.cond)
	- `ret_addr = val_a` (For RET, value of register X30)

How do we choose?
 ![[Program Counter Block Diagram.svg]]

### Instruction Memory

Instruction memory (can only be ***read*** by EL0 code)
- Indexed with byte address `imem_addr[63:0]`
- Returns instruction word `imem_rval[31:0]`. "Combinational".
- Asserts `imem_arr` if address is invalid


### Register File

- An edge-triggered D flip-flop corresponds to 1 bit of state
- A general purpose register is a collection of 64 such bits sharing a common clock, each storing 1 bit of the 64 bit data.
- Because data can be concurrently read and written to, we maintain a clock to store these values during execution and to stop race conditions.

![[Register File Block Diagram.svg|500]]

### ALU (Arithmetic Logic Unit)

- NZCV is in the ALU
- Con

### Data Memory

Can be read or written to, needs a clock.

Indexed with byte address `dmem_add[63:0]`
