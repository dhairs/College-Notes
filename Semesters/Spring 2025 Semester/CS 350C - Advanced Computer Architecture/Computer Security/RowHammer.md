
## Attack Patterns

- Single-sided attack
- Double-sided attack
- Multi-sided attack
	- Half-double
	- TRRespass

## Exploiting RowHammer

### Kernel Privilege Escalation

The basic idea is to use row hammering to induce a bit flip in a page table entry (PTE) that causes the PTE to point to a physical page table of the attacking process. This gives the attacking process read-write access to one of its own page tables, and hence to all of physical memory.


> [!faq] Why are bit flips exploitable?
> RowHammer-induced bit flips tend to be repeatable. This means that we can tell in advance if a DRAM cell tends to flip and whether this bit location will be useful for the exploit. 
> 
> We spray most of physical memory with page tables. This means that when a PTE's physical page number changes, theres a high probability that it will point to a page table for our process.


### Steps to Exploit

We need to search for useful bit flips:
- `mmap()` a large block of memory
- Search this block for aggressor/victim addresses by row-hammering random address pairs
- If we find aggressor/victim addresses where the bit flip isn't useful, skip that address set
- Otherwise, `munmap()` all but the aggressor and victim pages and begin the exploit attempt.

To exploit:
- Spray the memory with page tables
- Repeatedly `mmap()` a file in `/dev/shm` at 2 MiB-aligned virtual addresses (1 page table page worth of bytes)
- Cause kernel to populate some of the PTEs by accessing their corresponding pages (there are some clever tricks to randomize the kernel's allocations from physical memory)
- In the middle of doing all this, `munmap()` the victim page — the kernel will reuse this physical frame for a page table most likely
- Hammer the aggressor address
	- hopefully this induces the bit flip in the victim page

Then, check whether PTEs changed exploitably:
- Scan the mapped region to see whether any of the PTEs now point to pages other than the data file
- If there aren't any such PTEs, our attempt failed and we need to retry

Otherwise, we have gained illicit access to a physical page
- We need to check that it is containing a page table for our address space

## Defense Mechanisms

### Software Based

**Physical Isolation**:
- **CATT**: isolates user and kernel memory with guard rows
- **ZebRAM**: Uses zebra pattern to isolate critical data

**Attack Detection**: 
- **ANVIL**: Use HPMs
- **RADAR**: Monitors EM side channels

**Page Table Protection**:
- **CTA**: Cell-Type-Aware memory allocation
- **PT-Guard**: Message authentication codes for PTEs

### Memory Controller-Based

**Counter-Based**: TWiCe, Graphene

**Probabilistic**: PARA, Discreet-PARA

**Access throttling**: BlockHammer

### DRAM-Based

**Target Row Refresh** (TRR): Selectively refreshes potentially vulnerable rows, can be bypassed.

**Increased refresh rates**: Reduces window for successful attacks, though this has high performance and power costs

**In-DRAM ECC**: Single-Error Correction in DDR5, has new challenges (like error aliasing)