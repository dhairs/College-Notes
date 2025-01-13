## Why

There are a lot of troubles with memory partitioning:
- Fragmentation
- Need for compaction/swapping
- A process size is limited by the amount of physical memory still available

## What is Paging

Recall that there are many [[History of Memory Management#Fixed Partition Allocation|Partitioning]] techniques for memory management. 

Let's propose that instead of providing dynamic partitions, we provide a bunch of 'pages' in the system.

Each page is a pre-determined, static size. So, each request to memory is given a new page, which can then be used however we want. These pages don't have to be contiguous in physical memory. 

### Memory Frames

A memory frame is essentially a page, but instead of referencing virtual memory addresses, it references real addresses on the physical memory. 

**A key thing to note is that memory frames are always the same size as pages.** 

They are simply different names to refer to the same thing in different places. A page is in virtual memory, a frame is in physical memory.

### The Basic Solution

Give illusion of contiguous address space.

The actual allocation does not need to be contiguous.

Use a **Memory Management Unit (MMU)** to translate the illusory addresses to real, physical ones. 

The [[Virtual Addresses]] are mapped directly to different portions of physical memory, so the program accesses 'contiguous memory' in its virtual space, but can be accessing different **frames** (of the same size) of physical memory. This also allows for no external fragmentation in the physical memory.

However, because pages are essentially a type of [[History of Memory Management#Fixed Partition Allocation|Fixed Partition Allocation]], they are susceptible to internal fragmentation, since processes may not need the full space provided.

#### Key Facts

The physical address space is independent of the virtual address space:
- They can have different sizes, though uncommon
- 
The page size is always a power of 2 to simplify hardware addressing.

![[Paging Translation.svg]]

Because we don't have nearly as much memory as the virtual address space, some are not mapped to memory, and cause a `PAGE FAULT`.

#### Process' With Paging

![[Paging Process View.svg|400]]

### Boot Process

Because when the OS boots, there is no abstraction set up for virtual addressing, so it has to create that virtual address space. Then, the OS can also run in its own virtual address space.