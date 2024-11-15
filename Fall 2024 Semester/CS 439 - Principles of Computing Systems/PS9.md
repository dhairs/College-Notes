## **Problem 1**  
**A real disk does not have the same number of sectors per track. The number varies because the inner tracks do not have the same area as the outer tracks. So, outer tracks tend to contain more sectors than inner tracks. Consider a disk containing 1024 tracks, numbered from 0 to 1023, and where the number of sectors n per track t is given by the formula:**  
**n(t) = 1024 if t < 512, and**  
**n(t) = 1024 + 50t otherwise**  
**For a sector size of 512 bytes, and given that the disk has 4 double-sided platters, compute the capacity of the disk in bytes.**  

first 512: $512\times(1024)=524,288$

Next 512: $average = \frac{(50 * 1023) - (50 * 512)}{2}=12,775\times 1024=13,081,600$

So: $(13,081,600+524,288)*4 = 54,423,552 \text{ bytes}$

## **Problem 2**  
**A file system has a disk block of 8192 bytes and uses an indexing scheme where an index node contains 10 direct indexes, 1 indirect index, 1 level-2 indirect index, and 1 level-3 indirect index.**  

**Compute the amount of disk blocks required for the inode to represent a 1-GB file on a 64GB disk.**  

Total blocks: $\frac{1,073,741,824}{8192}=131,072$

10 direct, 1 indirect, 1 level 2 indirect, 1 level 3 indirect. So we need 3 because the third one is $(2^{10})^3=1,073,741,824$. We need 1 block for the single redirect  and 1 for the level 2 redirect. 

**3 blocks.**

## **Problem 3**  
**A "lease" is a lock on a file for a specified duration. When a process acquires a lease on a particular file, the operating system grants a lock to the process if it is not already held by another process. After the duration of the lease expires, the operating system revokes the lock and notifies the process via an upcall (signal). Describe a situation where the use of leases is superior to traditional locks.**  

This is useful for a situation where multiple systems may access the file system at once. it will prevent deadlock because it will ensure that the lock is given a program after a certain duration. This makes everything a little more robust.

## **Problem 4**  
**You are a member of a design team to build a backup tool for a UNIX system. One of your colleagues who did not attend CS 439H suggests that the tool can traverse the directory structure, marking all files that have been modified since the last backup by inspecting their timestamps. Then, all such files are then dumped on tape. Another colleague pleads with you to stop this insanity and design a better approach. Identify what is the problem with the proposed approach and outline a better decision mechanism to identify the files that need to be backed up. (hint: man cp).**

This is a bad solution because it is extremely slow, you have to access every single file and view it. Instead, it makes more sense to have something like a logfile in the OS that keeps track of changes that have occurred after, or even a checksum for files. the `cp` command, for example, uses the checksum comparison strategy to be able to quickly check whether or not files have been updated.