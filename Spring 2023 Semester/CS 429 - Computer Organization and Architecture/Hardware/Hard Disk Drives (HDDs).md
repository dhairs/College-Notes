## Anatomy of a Disk
Disks are made up of circular surfaces called "platters." The surface of these platters contain a large number of concentric **tracks**, which are each divided up into **sectors** divided by gaps. A sector is the smallest unit of data that can be read from or written to a disk. A **cylinder** is a collection of tracks on multiple surfaces that are located at the same radius. 

Early HDDs needed the physical address of a sector to be specified in the cylinder-head-sector (CHS) scheme. To a modern operating system, the HDD is a collection of logical sectors. 
- 300 [[Special Notation#Gigabyte (GB)|GB]] drive is sectors\[0:585,939,499\], each sector being 512 B 

These use the Logical Block Address (LBA) scheme. 

$\text{LBA}=(C\times\text{HPC}+H)\times\text{SPT}+S$, where $\text{HPC}$ is the number of heads per cylinder and $\text{SPT}$ is the number of sectors per track. The disk controller calculates the corresponding $(C,H,S)$ tuple from the $\text{LBA}$.

## Zone Bit Recording
The length of a track is proportional to its radius $r$. The angular velocity $\omega$ of all the tracks is the same (think back to high school physics). Therefore, the **linear velocity** $v=\omega r$ of an outer track is greater than that of an inner track (again, back to high school physics). This means there can be more sectors on an outer track than an inner track.