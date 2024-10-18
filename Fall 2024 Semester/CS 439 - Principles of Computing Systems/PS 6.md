1. Pages have (at least) the following three bits associated with them: the resident bit, the clock/reference bit, and the dirty bit. Describe each bit and its use.
	- The resident bit is used to define whether or not the page is currently loaded into main memory, or if it is only on the disk. This is useful for knowing if we need to pull the page and memory back into the main memory so we can allow the program to access it without a fault or accessing invalid memory.
	- The clock/reference bit is used for determining whether or not the current page has been accessed recently, and how recently. This allows a LRU type of eviction system, but the clock basically sets the bits to 0 every iteration.
	- The dirty bit is used to know whether or not the current page table has any changes that need to be synced to the disk before it can be evicted from main memory. This allows for validation.
1. What is the difference between global and local page replacement policies? Name a disadvantage of each.
	-  The global page replacement takes into account all pages in the system. This can cause processes that don't want their pages evicted to be unfairly taken by another process. 
	-  The local replacement policy only takes into account a process causing a fault's pages. This has the disadvantage of inefficient memory use.
    
3. Name two advantages of using small pages and two advantages of using large pages in a paging mechanism. Why are page sizes growing in paging memory systems?
	-  An advantage of using a small paging mechanism is that there is a lower risk of internal fragmentation, but this also causes slower reads because there can be more MMU tables to walk.
	- An advantage of using big pages is that the TLB and MMU can be faster due to less page table walks. This also reduces the size the page table uses in the system, saving memory.
	- In new systems, page sizes are growing because programs are getting larger and need more data to work, larger pages is simply a byproduct. Additionally, most new hardware is much more powerful and larger pages reduces performance drawbacks.
    
4. Consider a program with seven virtual pages numbered from 0 to 6 references its pages in the order:  
      
    0 1 3 6 2 4 5 2 5 0 3 1 2 5 4 1 0  
      
    Using clock page replacement algorithm with 4 frames and assuming demand paging, compute the number of page faults and show the state of frames (pages in frames and value of clock bit) after each page access.  

| Page Access | Page Fault? | Frames (Page, Clock Bit)    |
| ----------- | ----------- | --------------------------- |
| 0           | Yes         | (0, 1)                      |
| 1           | Yes         | (0, 1) (1, 1)               |
| 3           | Yes         | (0, 1) (1, 1) (3, 1)        |
| 6           | Yes         | (0, 1) (1, 1) (3, 1) (6, 1) |
| 2           | Yes         | (0, 0) (1, 1) (3, 1) (2, 1) |
| 4           | Yes         | (4, 1) (1, 1) (3, 1) (2, 1) |
| 5           | Yes         | (4, 1) (5, 1) (3, 1) (2, 1) |
| 2           | No          | (4, 1) (5, 1) (3, 0) (2, 1) |
| 5           | No          | (4, 1) (5, 1) (3, 0) (2, 0) |
| 0           | Yes         | (4, 0) (5, 1) (0, 1) (2, 0) |
| 3           | Yes         | (3, 1) (5, 1) (0, 1) (2, 0) |
| 1           | Yes         | (3, 1) (1, 1) (0, 1) (2, 0) |
| 2           | Yes         | (3, 0) (1, 1) (0, 1) (2, 1) |
| 5           | Yes         | (5, 1) (1, 1) (0, 1) (2, 1) |
| 4           | Yes         | (5, 1) (4, 1) (0, 1) (2, 1) |
| 1           | Yes         | (5, 0) (4, 1) (1, 1) (2, 1) |
| 0           | Yes         | (0, 1) (4, 1) (1, 1) (2, 1) |

    
5. Consider a two-level paging system with 128 pages and a page size of 256 bytes. The system has 2048 bytes of physical memory and is byte addressable. Assume the first-level page table holds 8 entries.
    1. How many bits are in a physical address?  
		-  The physical address has $\log_{2}(2048)=11$ bits.
        
    
    3. How many bits of the virtual address represent the first-level page table?  
	    - Because the first level table has 8 entries, we need $\log_{2}(8)=3$ bits.
        
    
    5. How many bits of the virtual address represent the second-level page table?  
	    - We need $\frac{128}{8}=16$ page entries because the first table has 8 entries, and we have 128 pages total. So, to address 16 entries, we need $\log_{2}(16)=4$ bits.
        
    
    7. How many bits are in the complete virtual address?  
	    - The complete virtual address needs the 3 bits from the first level, the 4 bits from the second level, and the offset, which is $\log_{2}(256)=8$, so $3+4+8=15$ bits.
        
    
    9. What size are the page frames?
		- The page frames are the same as the page size, $256$ bytes.