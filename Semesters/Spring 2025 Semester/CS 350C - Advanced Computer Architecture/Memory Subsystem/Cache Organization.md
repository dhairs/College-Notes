## Structure of a Cache



## Content Addressable Memory (CAM) Cells


## Cache Line Replacement Policy

Implementing replacement policies is difficult, even for moderate cache associativities. 

This makes no difference in a [[Cache Performance|direct mapped cache]] ($A=1$)

We can instead use 1 bit per set to keep track of MRU or LRU. At $A=2$, this increases to 3. At $A=3$, it reaches 3 bits per set. 


> [!FAQ] What about $A=4$?
> We need 5 bits to encode the $4!$ possibilities. 
> Bit 0: Way 1 MRU than Way 0.  
> Bit 1: Way 2 MRU than Way 0.  
> Bit 2: Way 3 MRU than Way 0.  
> Bit 3: Way 2 MRU than Way 1.  
> Bit 4: Way 3 MRU than Way 1.  
> Bit 5: Way 3 MRU than Way 2.
> We can build a FSM using this state encoding and two-bit encoding for the current access to determine next state and victim way. The theoretical minimum encoding of states requires $\lceil \log(4!) \rceil=5$ bits.

### Pseudo-LRU (Tree-PLRU)

An efficient algorithm to select and item that **most likely** has not been accessed recently, given a set of items and sequence of access events to the items.

This needs $A-1$ bits to represent the branch points of a binary decision tree. 

Results in a simple FSM for picking the victim way on a miss or updating the state on a hit in a given way.

## Advanced Cache Design Choices

If best-case cache access latency is still multiple processor cycles, we can improve throughput by designing a **pipelined cache**. 

If we have a cache miss, we can avoid stalling later memory operations by designing a **non-blocking cache**.

## Pipelined Cache

We will do this by adding pipeline registers between cache stages.

Read:
- Three-stage pipeline: access tag and data arrays, compare tags, select data block.

Write:
- Three-stage pipeline: access tag array, compare tags, write in data array.