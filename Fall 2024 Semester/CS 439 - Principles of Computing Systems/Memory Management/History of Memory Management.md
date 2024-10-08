## Early Systems

There was not much of an operating system. Not much memory either. It was just a program and a monitor, thus there was no protection or relocation.

![[Early Systems Memory Management.svg]]

## Overlaying

To overcome the fact that there was very limited memory space, a bunch of "optimizations" were made:
- Programs were written in pieces
- After each piece finishes, it 'loads' the next piece and then runs it
- Code in one overlay cannot access data or code in another overlay without loading it

This was horrendous to write programs for.

![[Overlaying Memory Management.svg]]

## Fixed Partition Allocation

This follows the idea that we can divide our memory into partitions of fixed sizes. Then, we can load a program into a partition. A program in a partition cannot access code in another partition. Something to note here is that the partitions are always fixed in size, so a program cannot exceed the memory given by the program.

![[Fixed Partition Allocation.svg]]

To fix the fact that there are programs with different requirements for memory, an approach that creates partitions with different sizes can be taken. This is still not efficient because no program purely fits into a fixed partition. Most of the time, there will be unallocated memory. E.g., loss due to internal fragmentation.

### Internal Fragmentation

![[Internal Fragmentation Fixed Partition.svg]]

Internal fragmentation occurs because a program leaves some of its memory space unallocated.

## Dynamic Partition Allocation

This comes as an upgrade to the fixed approach. Instead of having sizes that the programs have to choose to run in, why not provide them the ability to define the size they need?

This way, we can allocate memory depending on the program requirements and the partitions can adjust depending on the memory size. However, this approach requires code that is relocatable, working best with relocation registers.

## Buddy Allocation

This is what modern `malloc` implementations use.

To allocate a partition of $n$ bytes, the following steps are taken:
1. Divide the available space into two blocks (called buddies)
2. Recursively divide the first block in the same manner
3. Continue until we have the smallest block whose size is $> n$
