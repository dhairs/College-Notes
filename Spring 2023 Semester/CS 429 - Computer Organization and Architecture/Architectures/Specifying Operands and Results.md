## Instruction Processing

Recall how we define [[Instruction Set Architectures]].

1. Fetch 32-bit instruction word (IW) from memory location pointed to by program counter (PC)
2. Decode the instruction word
	- IW = (**operation**, *operands*, ==result== locations)
	- Read operands from registers
3. Execute arithmetic/logic for operation
	- Update NZCV 
4. Access memory *if needed*
	- Either a load or a store
5. Write ==results== back to registers *if needed*
6. Update [[AArch64 (ARM) State and Programming Model#^6298e8|Program Counter]] (PC) and [[SEQ - A Single Cycle implementation of chARM-v2#Architectural Status|Architectural Status]].

## Sources and Destinations

The generic form of an instruction is IW = (**operation**, *operands*, ==result== locations)

Operands can be:
- A constant value
- the contents of a register
- the contents of one or more memory cells
- R-Values

Results can be placed in:
- A register
- One or more memory cells
- L-values

## Operands
### Immediate Operands

This specification is used for constants that are directly embedded within the instruction

Assembly language syntax:
- `#-577`, `#0x1F`
- Range depends on instruction

### Register Operands

This specification is used for operands that are the contents of a register

Assembly language syntax:
- `Wn`, `Xn`: General purpose register (0-30) 
	- `W` tells us we only read the lower 32 bits of the register, *or*
	- We only write the lower 32 bits of the register and 0 the other values
- `WZR`, `XZR`: Zero Register
	- Returns zero when read, discards result when written
- `WSP`, `SP`: Current Stack Pointer

*Note that in all these cases the `W` is just signifying the 32-bit width operation*

### Memory Operands

This specification is used for operands that are the contents of one or more memory locations. Only relevant for load/store instructions.
- How wide? Encoded by the [[Instruction Set Architectures#^394cf4|opcode]] (`LDUR{[B|H|SB|SH|SW]}`). Call this width $b$ in bytes.
	- `H` is half the word size
- From which memory location? There's too many choices, and we might want different locations from the same code. **So**, we use a formulaic way of determining the location.

The formulaic way of determining the location of memory is given by the formula, called the **addressing mode**, which is encoded into the instruction.

This formula is evaluated in the **Execute Step** of instruction processing to provide a value called the **effective address** (EA). We call this value $a$.

The effective address is used to read from/write to $\text{BOX}(a, a+b-1)$ ([[Objects and Names#^b3b72c|BOX Definition]]) in the **Memory Stage** of instruction processing.

### Examples of Instructions

Different flavors of `ADD` instructions:
- `ADD W0, W1, W2`
	- We are taking the values of `W1` and `W2`, adding them, and writing them to `W0`
- `ADD X0, X1, X2`
	- We are taking the values of `X1` and `X2`, adding them, and writing them to `X0`
- `ADD X0, X1, W2, SXTW`
	- `SXTW` means **sign extend word**. It extends the 32 bit to a 64 bit
	-  We are taking the values of `X1` and `W2`, adding them as 64 bit numbers, and writing them to `X0`
- `ADD X0, X1, #42`
	- We add the 64 bit number in `X1` to the immediate (constant) in `#42`, and put the result in the register `X0`

## A64 Load/Store Addressing Modes

|  | Offset |  |  |
| ---- | ---- | ---- | ---- |
| **Addressing Mode** | **Immediate** | **Register** | **Extended Register** |
| Base register only | `[base{, #0}]` |  |  |
| Base plus offset | `[base{, #imm}]` | `[base, Xm{, LSL #imm}]` |  |
| Pre-indexed | `[base, #imm]!` | `[base, base + #imm]` |  |
| Post-inedexed | `[base], #imm` | `[base], Xm` |  |
| Literal (PC-relative) | `label` |  |  |

