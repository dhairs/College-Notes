Discussion Section Problem Set #: 5
Student Name: 
EID: 

1. What is a virtual address? What is a physical address? How do they relate to each other?


A virtual address is an address used by programs in their own address space to access memory. A physical address is real memory addresses on the main memory of the system. They are related because virtual addresses are mapped to physical addresses by the Operating System to maintain isolation between processes.


2. What causes a page fault? What is the end result for the running process?

A page fault is caused when a process tries accessing a virtual address not yet mapped to a physical address. 


3. What causes a memory exception? What is the end result for the running process?

A memory exception is caused when a program tries to access memory that it is not allowed to touch or that doesn't exist. This is like a SEGFAULT. The end result is that the operating system terminates the process because it is dangerous to allow it to keep running.


4. Name two advantages of paging over relocation.

Paging is better than relocation because it causes less external fragmentation. Additionally, it makes it easier for processes to share the same pages for things like global DLLs.


5. Assume you have a virtual memory system that uses paging. Is the system vulnerable to internal and/or external fragmentation? Explain.

Yes. The system can still have internal fragmentation because the page size is fixed and that means that there will be wasted space within each page. There will, however, not be external fragmentation because pages don't have to be contiguous in memory.


6. Consider a paging system with 16 pages and a page size of 256 bytes. The system has 1024 bytes of physical memory. How many bits are in a physical address? How many bits represent the page number? How many bits are in the complete virtual address? What size are the page frames?

There are log_2(1024) = 10 bits in a physical address. Because there are 16 pages, we need log_2(16) = 4 bits to represent the page number. In the virtual address, we have to get the bits for a page number (which is 4) and the offset inside that page. So, since our pages are 256 bytes, we need log_2(256) = 8 bits to represent the offset. We then need 12 bits. The page frame size is the same as the page size, so also 256 bytes.