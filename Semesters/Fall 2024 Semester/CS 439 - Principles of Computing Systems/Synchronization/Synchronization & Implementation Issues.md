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

### Starvation

If the synchronization solution is not well implemented, a thread may starve.

EX: A semaphore implemented in LIFO order (a stack)

### Deadlocks

There are 4 conditions that **must** be true for deadlock to occur, they are:
1. **Mutual Exclusion**: A process or thread must be the only one able to access a resource, forcing others to not be able to use it
2. **No Preemption**: A resource can only be given up when the holding process wants to, it can not be preempted to do so
3. **Circular Wait**: A process waits for a resource held by another process, which is also waiting for the original process to release the resource
4. **Hold and Wait**: A process is holding onto a resource and requesting/waiting for a resource held by another process.

#### Example

| Thread 1 | Thread 2 |
| -------- | -------- |
| P(s1)    | P(s2)    |
| P(s2)    | P(s1)    |
| V(s1)    | V(s2)    |
| V(s2)    | V(s1)    |
In this case, the threads both need to access s1 and s2, which leads them into a deadlock.