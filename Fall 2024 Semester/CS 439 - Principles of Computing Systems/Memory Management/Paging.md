## Why

There are a lot of troubles with memory partitioning:
- Fragmentation
- Need for compaction/swapping
- A process size is limited by the 

## What is Paging

Recall that there are many [[History of Memory Management#Fixed Partition Allocation|Partitioning]] techniques for memory management. 

Let's propose that instead of providing dynamic partitions, we provide a bunch of 'pages' in the system.

Each page is 

### The Basic Solution

Give illusion of contiguous address space.

The actual allocation does not need to be contiguous.

Use a Memory Management Unit (MMU) to translate the illusory addresses to real, physical ones. 

![[Paging Translation.svg]]