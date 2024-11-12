
## Flat File System

A fat file system consists of an array of index nodes (or "i-nodes")

There is one i-node per file, which contains

![[iNode]]

### File Allocation Table (FAT)

### Indexed Allocation


### Free Space Management

**Bit vectors**:
- A bit for each block, 1 for available, 0 otherwise

**Linked Lists**:
- Link al free blocks in one list