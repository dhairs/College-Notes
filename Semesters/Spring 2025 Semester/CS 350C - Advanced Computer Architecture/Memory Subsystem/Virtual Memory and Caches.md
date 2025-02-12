
## Caches and Addressing

The process issues a virtual address (VA) in connection with a memory access. The memory subsystem deals with physical addresses (PAs). The virtual memory subsystem in the OS performs the $\text{VA}\to \text{PA}$ translation. 

Caches perform two functions to identify a hit/miss:
1. Indexing
2. Tag matching

> [!faq]- How does address translation interact with data caching?
> ![[Virtual and Physical Tagged Cache.svg]]
> Generally, it is preferred to use the VIPT variant in L1 caches because the index is available pre-translation.

## Issues to Consider

Flushing of caches on a context switch: use PID as part of the tag.

Aliasing: two different VAs for the same PA.
- Use page coloring ("set associative mapping for VM")

MMIO
- Typically uses physical addresses