## Mapping Pages to Memory

Recall [[Paging]]. We need to have [[Virtual Addresses]] to be able to manage each processes individual memory needs. How do we map the virtual pages into real, physical memory?

Page tables are the answer.

### A Simple Abstraction for Page Tables

Page tables can be seen as a simple one-to-one memory mapping for pages to physical memory:

![[Page Table Abstraction.svg]]

## Page Table Structure

Page tables are indexed by a virtual page number. It contains the frame number (if any). In addition, it contains protection bits and a reference bit.


| Frame No. | Valid Bit | Write Bit | Read Bit | eXecute Bit | reFerence Bit | Modified Bit |
| --------- | :-------- | --------- | -------- | ----------- | ------------- | ------------ |
| \#        | v         | w         | r        | x           | f             | m            |

The valid bit can be used to let us know when the page is in main memory, or if it is only on the disk.