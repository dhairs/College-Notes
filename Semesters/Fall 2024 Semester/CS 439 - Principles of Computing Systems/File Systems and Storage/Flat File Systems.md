
## Understanding Flat File Systems

A fat file system consists of an array of index nodes (or "i-nodes" or "inode")

There is one i-node per file, which contains

![[inode.svg]]

### File Allocation Table (FAT)

### Indexed Allocation


### Free Space Management

**Bit vectors**:
- A bit for each block, 1 for available, 0 otherwise

**Linked Lists**:
- Link all free blocks in one list

### Sparse Files
This is conceptual, but a file can have empty "holes". Supposedly better for debugging or something. Useless, but supported in file systems.

You can't use this with sequential or linked allocations.

### File Blocks

Not exactly a [[Disks|disk or SSD sector]]. 

Tradeoffs are similar to pages:
- If we have larger blocks, we can locate them quicker
- If we have larger blocks, we don't have to do a lot of disk accesses to get an inode

### Optimization for SSDs

Exploit the low latency
- No need to worry about disk seeks or rotational latency
- Reduce the number of writes or amount of data to be written (e.g., use compression)

Use the TRIM command
- SSD controllers rework the allocation to reduce wear leveling and do garbage collection to reduce the write inflation factor

### File Extent

Allocate files in extents (what is an extent??)

An extent is a group of consecutive block numbers

Metadata: a start and number of blocks

More efficient for access and lower overhead (used by EXT4, APFS, etc.)
