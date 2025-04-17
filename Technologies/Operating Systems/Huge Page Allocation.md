## History

Recall the history of [[Page Tables]]

### Heuristic for Promotion

**FreeBSD**: Multiple huge page sizes, reserves contiguous and defers promotion


## HawkEye

HawkEye has 4 major advancements:
- Asynchronous Page Zeroing
	- Bypass allows for performance
	- Free list and Non-zero list
- Dissolution of memory bloat
	- Break apart pages with too many zero baseline pages
	- Bloat-recovery thread activates at high memory pressure, checks whether or not a threshold pages are zeroed or not, if not, breaks them up.
- Fine-grain promotion
	- Tracks which base pages in huge page regions are "hot" and places them in buckets
	- Promotes pages with higher TLB pressure
- MMU Overhead
	- Per-process allocation is done by priority of MMU overhead (hardware/software) or buckets

Even with software-only HawkEye-G, there are massive improvements in runtime.

Especially useful for virtualization.

### CBMM

All kernel operations have a cost-benefit to the userspace. They utilize models to express page promotion, zeroing, and eager paging.