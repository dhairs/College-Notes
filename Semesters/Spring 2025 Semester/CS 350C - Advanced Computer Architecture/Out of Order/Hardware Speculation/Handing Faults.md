## Fault Handling

Lump together possible fault-generating events: mispredicted branches, interrupts, exceptions, system calls.

Set the exception bit of the **relevant** ROB entry. 
- **Relevant**: for interrupts, head of ROB; for all others, the actual instruction.