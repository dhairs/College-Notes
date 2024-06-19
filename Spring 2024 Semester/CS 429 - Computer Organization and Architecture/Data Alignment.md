
## Memory Buses

Buses are fixed widths (e.g, 8-byte bus width, so 8 bytes can be sent at once)

The main memory is organized into banks, each of a certain amount of bytes

Fetching 8 bytes from an arbitrary memory address (that happens to span multiple banks) can be arduous, and uses a lot of time and resources
- We either send 2 8-byte quantities and have it reassembled on reception, or
- Assemble them at the memory level before sending them through the bus

## Why Align Data?

Computers have restrictions on the placement of data objects in memory so they can simplify high-performance memory system design

This restriction is given to be enforced by the compiler
- AArch64 requires all to be 4-byte aligned

## Defining Data Alignment

An object `x` of a **basic data type** is said to be aligned $\text{iff}$ `ADDR(x) mod SIZE(x) = 0` (so `ADDR(x)` is a multiple of `SIZE(x)`)

So, for this reason, a `char` can be located at any byte address, a `short` has to be on an even byte address, `int`'s must be on multiples of 4, and etc.

An object `x` of pointer type can be located at a byte address that is a multiple of [[Operations on Representations.md#Word Size|word size]] (8 on most machines)

An aggregate object `x` of a **derived data type** `T` is said to be aligned $\text{iff}$ 
- **Sub object rule**: every sub-object of the type is recursively *aligned*
- **Array rule**: every element of an object `y` of type "array of `T`" is *aligned*

## Managing Data Alignment

We have to make 2 decisions for every object `x`:
 - What is `ADDR(x)`?
 - What is `SIZE(x)`?

For basic types, we only need the `ADDR(x)`

For derived types we need to decide both


