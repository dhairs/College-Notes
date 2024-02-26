## Where are Variables Stored?

Local variables are stored in the function's stack frame
- The typical addressing mode is `[SP, #pimm]`

Global variables are stored at locations named by labels
- The typical addressing mode is `label`
- Need to use `ADRP` and `ADR` instructions to reach the address