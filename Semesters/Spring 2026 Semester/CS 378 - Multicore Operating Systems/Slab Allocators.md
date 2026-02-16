## What is a Slab

A slab is an array of contiguous pages in memory, partitioned into different, constant-size slots. These slots are sized by powers of 2. This prevents internal fragmentation since its fixed and meant to be allocated as this.

Similar to malloc implementation, uses free lists and pointers to ensure connection.

Each core owns a slab of each object size so that we reduce contention and race conditions.