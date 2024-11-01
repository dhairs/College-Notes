
1. Disk requests come into the disk driver for tracks 10, 22, 20, 2, 40, 6, and 38, in that order. A seek takes 0.5 + 0.6/track msec. How much seek time is needed for the following scheduling algorithms?  
	a. FIFO: $((20-10) + (22-10) + (22-20) + (20-2) + (40-2) + (6-2) + (38-6))*(0.5+0.6)=150.6ms$
	b) SSTF: $((22-20)+(22-10)+(10-6)+(6-2)+(38-2)+(40-38))*(0.5+0.6)=66ms$
	
	c) LOOK (Identical to SCAN but doesn't move to the end): $((22-20)+(38-22)+(40-38)+(40-10)+(10-6)+(6-2))*(0.5+0.6)=64ms$ 
	In all cases, the arm is initially at track 20.  
2. We would like to build a 20TB HDD. We have access to a platter that consists of 131072 tracks, and each track consists of 4096 sectors. The sector size uses the Advanced Format  (AF). Is it possible to build the HDD, given that the maximum standard package today for an enterprise HDD cannot exceed 8 platters? 

	 $131072\times{4096}\text{ sectors} \times{4096}\frac{\text{bytes}}{\text{sector}}=2tb$. Then, we can multiply by the number of platters, which is 8. $8*2=16$ terabytes. So no, you cannot make a 20TB HDD with these specifications.
	
3. A 1TB QLC consists of 128KB blocks and a page size of 4KB. Answer the following questions:  
	a. How many floating gate cells are needed for this device?  
		QLC, so 4 bits per cell. Total bits is $2^{40}\times 8 \frac{\text{bits}}{\text{byte}}\times 1024 \frac{\text{Kb}}{\text{Mb}} \times 1024 \frac{\text{Mb}}{\text{Gb}} \times 1024 \frac{\text{Gb}}{\text{Tb}}=8 \times 2^{80} \text{ bits}$
		We then need $2^{40} \times 2$ cells
	b. How many pages are contained in this device?  
		$\frac{2^{40}}{4096}=268,435,456$ pages
	c. How many pages are contained per block?  
		$\frac{128}{4}=32$ pages
	d. Consider block 3 which contains 14 valid pages, and we wish to update page 2 with new content (page 2 is marked as valid). How many total writes will be needed to perform the update? What is the write amplification factor in this case? 

	 You need to read the whole block, erase the whole block, and then write the newly modified block. As a result, you need 32 reads (all 32 pages in the block) and 32 writes (all 32 blocks). SO there will be **32 writes.**
4. A RAID-4 system consists of five 10TB HDDs. Answer the following questions:  
	a. If disks are numbered 0 through 4, which disk contains block 314?  
		$314\%5=4$. Block 314 is on disk 4.
	b. How many disk accesses will be involved if we wish to update byte 79 in block 314?  
		We need to read the block from disk 4, then read the parity, then calculate a new parity, then update the block, then update the parity. So 5 disk accesses.
	c. What is the usable storage that is available to users of this system? 
		Because 1 disk is reserved for parity, it should be $5-1=4\times 10\text{TB}=40\text{TB}$ usable storage.  
	d. If this system is reconfigured as a RAID-6 system, repeat part (c).  
		2 parity disks, so $5-2=3\times 10\text{TB}=30\text{TB}$.
5. We would like to build a RAID system out of SSDs. Which RAID level would you recommend, and why?
	1. **Raid level 5 or 6 would be best because there is limited write amplification, since you write across disks for parity, so you are keeping usage level. **