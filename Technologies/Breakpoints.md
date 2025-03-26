## How to breakpoints actually work?

The debugger looks at the binary of the program you are running, finds the place you put a breakpoint, and puts a trap instruction. Then, the hardware needs to expose an API for the debugger to read CPU architectural state. See [[Handling Faults]].