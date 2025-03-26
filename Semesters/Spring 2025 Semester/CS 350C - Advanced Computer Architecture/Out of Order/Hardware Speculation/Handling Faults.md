## Fault Handling

Lump together possible fault-generating events: mispredicted branches, interrupts, exceptions, system calls.

Set the exception bit of the **relevant** ROB entry. 
- **Relevant**: for interrupts, head of ROB; for all others, the actual instruction.

![[Fault Exception Entry.svg]]

The exception handler entry keeps track of PC, nextPC, the exception type, if it finished, the preg, and if excepted.

If instruction at head of ROB has exception bit set, then flush pipeline state and take appropriate action. 

| Exception           | Action                                                        |
| ------------------- | ------------------------------------------------------------- |
| Mispredicted branch | See [[Handling Branches]]                                     |
| Interrupt           | Load Interrupt Handler                                        |
| Exception           | Invoke Exception Handler                                      |
| System Call         | Invoke exception handler to jump to privileged execution mode |

> [!FAQ] What program state needs to be preserved on an ROB flush?
> We need the Next PC 
> 
> Memory state as of last committed instruction
> 
> Architectural register state as of last committed instruction

Components of state that need to be recovered:
- Next PC is available from the ROB entry of the last committed instruction
- Memory state is handled by sending only stores to memory when they are no longer speculative
- Architectural register state can be recovered using the [[Multiple-Issue Processor#Register Alias Table (RAT) (AKA Register Rename Table)|RAT]]. How do we do this efficiently?

### Retirement Register File (RRF) (Approach 1)

Keep a small register file (of size 16 in this example) in the commit stage. This is the RRF. At commit time, we update the corresponding architectural register in the RRF. Each ROB entry thus needs to have new fields: value produced by the instruction (64 bit) and the ID of the destination register. 

We once again have to worry about commit widths of greater than 1. Covered in [[Multiple-Issue Processor]].

Restoring the table involves transferring the entire contents of the RRF to the regular register file with appropriate changes made to the rename table. Since we are initializing from a clean state, we can transfer the contents of **architectural** register $r_{i}$ in the RRF **to** **physical** register $p_{i}$ and create a corresponding mapping.