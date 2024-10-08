## Diagram

The Storage Hierarchy of a Computing system can be seen as:

![[Computing Storage Hierarchy.svg]]

## Properties of the Hierarchy

The Price per bite (Price/byte) goes down as you move up in the hierarchy:

### Speed
L1 access time is 1 or 2 CPU cycles
L2 access time is in the 10s of CPU cycles

Main memory access time is in the 10s of nanoseconds (ns) (typically is 60 or more)


### Sizes

L1 cache has a small amount of storage, typically 8 to 64K bytes

L2 is smaller, usually ranging between 256K and 2M bytes

## Programmer's View of the Storage Hierarchy

Programmers assume that the memory is just an array of bytes. They assume that it is **addressable in a linear fashion**. Memory cannot hold values between program runs.

### Relocatable Programs

Because address spaces can be different each run time for the same program, it is important to make sure that the program works with memory changes. 

These are programs that:
- Do not assume anything about where they will be loaded and do not assume anything about where the data is placed
- A linker can prepare them to run anywhere

#### Implementations

There's a few ways you can implement relocation:
1. Relocating linker
2. Relocating loader
3. Relocation register

##### Relocating Loader

The same as a relocating linker, except that it resolves the references at load time. 