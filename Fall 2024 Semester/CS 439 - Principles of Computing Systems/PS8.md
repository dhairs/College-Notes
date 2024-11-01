
1. Disk requests come into the disk driver for tracks 10, 22, 20, 2, 40, 6, and 38, in that order. A seek takes 0.5 + 0.6/track msec. How much seek time is needed for the following scheduling algorithms?  
	a. FIFO: $((20-10) + (22-10) + (22-20) + (20-2) + (40-2) + (6-2) + (38-6))*(0.5+0.6)=150.6ms$
	b) SSTF: $((22-20)+(22-10)+(10-6)+(6-2)+(38-2)+(40-38))*(0.5+0.6)=66ms$
	
	c) LOOK (Identical to SCAN but doesn't move to the end): $((22-20)+(38-22)+(40-38)+(40-10)+(10-6)+(6-2))*(0.5+0.6)=64ms$ 
	In all cases, the arm is initially at track 20.  
2. We would like to build a 20TB HDD. We have access to a platter that consists of 131072 tracks, and each track consists of 4096 sectors. The sector size uses the Advanced Format  (AF). Is it possible to build the HDD, given that the maximum standard package today for an enterprise HDD cannot exceed 8 platters? $131072\times{4096}\text{ sectors}\times_{4}$ 
3. A 1TB QLC consists of 128KB blocks and a page size of 4KB. Answer the following questions:  
	a. How many floating gate cells are needed for this device?  
	b. How many pages are contained in this device?  
	c. How many pages are contained per block?  
	d. Consider block 3 which contains 14 valid pages, and we wish to update page 2 with new content (page 2 is marked as valid). How many total writes will be needed to perform the update? What is the write amplification factor in this case?  
4. A RAID-4 system consists of five 10TB HDDs. Answer the following questions:  
	a. If disks are numbered 0 through 4, which disk contains block 314?  
	b. How many disk accesses will be involved if we wish to update byte 79 in block 314?  
	c. What is the usable storage that is available to users of this system?  
	d. If this system is reconfigured as a RAID-6 system, repeat part (c).  
1. We would like to build a RAID system out of SSDs. Which RAID level would you recommend, and why?
	1. **Raid level 5 or 6 would be best because**