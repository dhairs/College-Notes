
## The Compilation Process

Remember our [[Toolchain]], we use `gcc` and `gdb`, and some other tools. 

When we have something like `gcc -g -o p p1.c p2.c`

This is really what happens:

![[GCC Compilation Process]]


## The Instruction Set Architecture (ISA)

The definition of the format and behavior of machine-level programs (object modules and executables)
- To do this, we need to have a way of keeping track of machine state
- We define how instructions can change the machine state

So, this is the **formal contract/interface** between the hardware and software

## Important Interfaces

The operating system is the **manager** of most tasks. It facilitates what other programs are able to do. This is why we need to make a call to `sbrk` through the OS to get memory, instead of being able to do it ourselves.

**ISA is interfaces 3 and 4**
- Interface 3: System ISA. Higher privilege.
- Interface 4: User ISA. Lower privilege.

Interface 2: System calls (`sbrk`)

Application Binary Interface (ABI): interfaces 2 and 4

Interface 1: High level library calls

Application Programming Interface (API): interfaces 1 and 4

![[ISA Architecture.png]]

## Machine and Assembly Languages

Machine language is just a bunch of bit strings encoding instructions, e.g. `0xF84103E0`

Assembly language: Symbolic representation of machine language in human-"friendly" form
- Textual rather than binary, e.g. `LDUR X0, [SP, #16]`
- Specifications of operands may differ from their machine-language encoding (Shift operand in `MOVK` and `MOVZ`)
- Convenient aliases for special cases (`LSL` (Logical Shift Left) and `LSR` (Logical Shift Right) for `UBFM` (Unsigned Bit Field Move)) ("**pseudo instructions**")

Assembly is basically just syntactic sugar for machine language.

## Instructions

At the representation level, an instruction is a bit string that is interpreted as a verb rather than as a noun.

Semantically, the verb that the instruction denotes maps machine states to machine states. 

An instruction **must** specify (at the very least):
- **Source operands**: what inputs (aka operands) it needs (how many of them, how wide they are, where they come from)
- **Operation Code (opcode)**: What operation it performs on the inputs.
- **Destination**: Where the output (result) goes | *note this is the machine state change*
- **Side effects**: what side effects, if any, do occur?

## Fixed Program Computer

A fixed program computer is designed for a particular task — hard to reprogram. Reprogramming either may not be possible, or it is at least complicated
- Think of calculators, cash registers, etc.

## Stored Program Computer

A stored program computer includes an instruction *set* by design, and can store in memory a series of instructions (the program) that describes the computation.

No distinction between data and code.

Started by Turing in 1936.