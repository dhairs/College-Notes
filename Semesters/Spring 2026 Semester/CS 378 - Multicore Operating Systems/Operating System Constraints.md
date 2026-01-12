## Design Constraints

### Architecture Support
- Any architecture, we get to choose
	- 64-bit is standard
- x86, ARM, RISCV, MIPS, SPARQ, POWERPC, etc.
- Don't need to pick and know what arch to support from the start
	- Can be changed

### Platform

Need to pick platform being run on in addition to the architecture. (e.g. Raspberry Pi for ARM).

RPi3/4 may require implementing a USB specification to be able to access networking. 
- Could always take a look at Linux's USB driver to find out how to do it

It IS okay to find other drivers online and make them work here.

### Hardware or Emulation

Using emulators is useful for development and quick turnaround in testing. (QEMU is the standard for the most part).

Need to run on hardware in a meaningful way to be able to get an A in this course

