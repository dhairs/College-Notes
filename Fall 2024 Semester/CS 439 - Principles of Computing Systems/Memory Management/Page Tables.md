## Mapping Pages to Memory

Recall [[Paging]]. We need to have [[Virtual Addresses]] to be able to manage each processes individual memory needs. How do we map the virtual pages into real, physical memory?

Page tables are the answer.

Note that **each process has its own page table**.

It lives in the Process Control Block (PCB) or Process Descriptor.

### A Simple Abstraction for Page Tables

Page tables can be seen as a simple one-to-one memory mapping for pages to physical memory:

![[Page Table Abstraction.svg]]

## Page Table Structure

Page tables are indexed by a virtual page number. It contains the frame number (if any). In addition, it contains protection bits and a reference bit.


| Frame No. | Valid Bit | Write Bit | Read Bit | eXecute Bit | reFerence Bit | Modified Bit |
| --------- | :-------- | --------- | -------- | ----------- | ------------- | ------------ |
| \#        | v         | w         | r        | x           | f             | m            |

**Necessary Bits**:
- v: The valid bit can be used to let us know when the page is in main memory, or if it is only on the disk.


**Optimization Bits**:
- r: The reference bit is set to 1 whenever the page is read or written to.
- m: The modified bit is set to 1 whenever the page is modified.

In the data segment of a process:

| Frame No. | Valid Bit | Write Bit | Read Bit | eXecute Bit | reFerence Bit | Modified Bit |
| --------- | :-------- | --------- | -------- | ----------- | ------------- | ------------ |
| \#        | v         | 0         | 1        | 1           | f             | m            |

### Allowing for JIT Compilation

Just-in-Time (JIT) compilation needs to be able to edit the code, for languages like Java and Python, etc. But because we keep track of an execute bit so that we prevent stack overflow and other code modifying bugs, we can't exactly just write new code onto the stack.

So, we add our newly compiled code to the heap, and tell the OS that this part of the heap should be executable. 

## Defined Structure

![[Page Table Actual.svg]]

Each page will have its own virtual private number. It will use that to find it's index in the page table, which will then be used to find the frame number in physical memory.

