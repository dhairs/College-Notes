## Anatomy of a Disk

Disks are made up of circular surfaces called "platters." The surface of these platters contain a large number of concentric **tracks**, which are each divided up into **sectors** divided by gaps. A sector is the smallest unit of data that can be read from or written to a disk. A **cylinder** is a collection of tracks on multiple surfaces that are located at the same radius. There are two **read/write** heads **per platter**.

Early HDDs needed the physical address of a sector to be specified in the cylinder-head-sector (CHS) scheme. To a modern operating system, the HDD is a collection of logical sectors.

- E.g., if we have a 300 [[Special Notation#Gigabyte (GB)|GB]] drive with sectors\[0:585,939,499\], each sector would be 512 B

These use the Logical Block Address (LBA) scheme.

$\text{LBA}=(C\times\text{HPC}+H)\times\text{SPT}+S$, where $\text{HPC}$ is the number of heads per cylinder and $\text{SPT}$ is the number of sectors per track. The disk controller calculates the corresponding $(C,H,S)$ tuple from the $\text{LBA}$.

## Zone Bit Recording

The length of a track is proportional to its radius $r$. The angular velocity $\omega$ of all the tracks is the same (think back to high school physics). Therefore, the **linear velocity** $v=\omega r$ of an outer track is greater than that of an inner track (again, back to high school physics). **This means there can be more sectors on an outer track than an inner track.**

In reality, we don't do this for every track, but the number of sectors per track for a group of adjacent tracks. This grouping is called a **zone.**

Disk throughput is constant within a zone, and decreases from outer to inner tracks.

## Capacity

There are a few parameters to keep track of when determining the capacity of an HDD:

**Recording Density**: Bits per inch (BPI) - number of bits on a 1" (inch) circumferential segment of track.

**Track Density**: Tracks per inch (TPI) - number of tracks on 1" (inch) radial segment of disk

**Areal Density**: Bits per inch$^2$ - recording $\text{density}\times\text{track density}$.

### Capacity Formula

$$
\text{C} =\frac{\text{\# bytes}}{\text{sector}}\times \frac{\text{(avg \# sectors)}}{\text{track}} \times \frac{\text{\# tracks}}{\text{surface}} \times \frac{\text{\# surfaces}}{\text{platter}} \times \frac{\text{\# platters}}{\text{disk}}
$$

#### Example

Five double-sided platters; 512 B sectors; 20,000 tracks/surface; 300 sectors/track on average

What is the capacity?

$$
\begin{align}
\frac{512\text{B}}{\text{sector}} \times \frac{300\text{ sector}}{\text{track}} \times \frac{20{\small,}000\text{ track}}{\text{surface}}\times \frac{2\text{ surface}}{\text{platter}}\times 5\text{ platter} \\
 = 30{\small,}720{\small,}000
{\small,}000\text{ B} = 30.72\times 10^9\text{ B}= 30.72\text{ GB}
\end{align}
$$

Make **sure** you use [[Special Notation#Gigabyte (GB)|Gigabytes]]|, **_not_** [[Special Notation#Gibibyte (GiB)|Gibibytes]].

### Access Time

#### Components of Access Time

Access time = seek time + rotational latency + transfer time.

**Seek time**: $T_{\text{seek}}$ is the time taken to move the arm to the track containing the desired sector (overhead). This depends on the previous position of the head.

**Rotational latency**: $T_{\text{rot}}$ is the time taken for the target sector to arrive under the head (overhead).

**Transfer time**: $T_{\text{tsr}}$ is the time taken to read/write the contents of the sector (productive).

#### Access Time Formulas

$T_{\text{rot}}(\text{MAX})=\frac{1}{\text{RPM}}\times \frac{60\text{ s}}{1\text{ min}}$

$T_{\text{rot}}(\text{AVG})=\frac{1}{2}\times T_{\text{rot}}(\text{MAX})$

$T_{\text{tsr}}(\text{AVG})=\frac{1}{\text{RPM}}\times \frac{1}{\text{average \# of sectors per track}}\times \frac{60\text{ s}}{1\text{ min}}$

#### Example

Disk parameters: 512 B sectors, 400 sectors/track on average; 7,200 rpm; average seek time of 9 ms.

$T_{\text{rot}}(\text{AVG})=\frac{1}{2}\times \frac{1\text{ min}}{7,200\text{ rev}}\times \frac{60,000\text{ ms}}{1 \text{ min}}=4.17\text{ ms}$

$T_{\text{tsr}}(\text{AVG})=\frac{1\text{ min}}{7,200\text{ rev}}\times \frac{60,000\text{ ms}}{1 \text{ min}}\times \frac{1\text{ track}}{400\text{ sectors}}=0.02\text{ ms}$

$T_{\text{access}}(\text{AVG})$:

$$
\begin{align} \\
T_{\text{access}}(\text{AVG})=T_{\text{seek}}+T_{\text{rot}}+T_{\text{tsr}} \\
=(9+4.17+0.02)\text{ ms} \\
=13.19\text{ ms}
\end{align}
$$

### Average Head Seek Distance

For a disk of $N$ tracks, the average seek distance is 

$$
\frac{1}{3}\times\left( N-\frac{1}{N} \right)
$$

## Reliability

**Mean Time To Failure (MTTF)**: usually in hundreds of thousands or millions of hours

Sectors contain **Error Correction Codes (ECC)** (think [[Main Memory#Hamming Codes|Hamming Codes]] for example)

Dual porting for host-failure: two machines could be connected to the same disk

**Bad Sectors**: The disk often comes with ad sectors, the system has to account for them when setting up the disk. It needs to remap those sectors into another space. As a result, the interface masks them.

## Contiguous Sectors

Physically contiguous sectors cannot be read in one singular seek, there is data transfer overhead.

However, logically contiguous sectors are usually physically spaced apart (e.g., every other or every third)

Organizing data such that they can be read sequentially is **key** to the performance in disk systems.

## Disk Head Scheduling

Assuming there are several requests available, there are a few schemes to schedule how the disk head moves:
- **First Come First Serve (FCFS)**
- **Shortest Seek First (SSF)**: go to the nearest track first
- **SCAN**: Start from track 0, handle the requests in order until the outer track, and restart from 0 again (essentially a loop from in to out). Not amazing, keeps going to the end of the track even when there are no more requests
- **Loop**: Same as SCAN, but stops once there are no more requests on the outer.
- **Elevator**: The same as SCAN, but reverse motion after reaching the last request, and starts at the first requested track.
- **Priority Based** (very rare): Different priorities, used in things that need real time requirements