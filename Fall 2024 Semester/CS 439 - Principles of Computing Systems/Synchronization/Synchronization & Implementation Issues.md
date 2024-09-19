## Problems

Quite a few:
- Performance
- Interaction with thread priorities
- Deadlocks
- Starvation
- Synchronization priorities

### Performance

Blocking synchronization
- Context switch if the mutex is not available
- Makes CPU available to others

Spin-lock synchronization
- Wastes CPU resources
- But if mutex is available, or will be soon, then we avoid the context switch overhead

Hybrid Synchronization (Solaris)
- Starts out with a spin-lock
	- if mutex is available, enter the [[Problems with Concurrency#Critical Sections|critical section]]
- Spin for a limited time, if mutex is not available, use blocking synchronization