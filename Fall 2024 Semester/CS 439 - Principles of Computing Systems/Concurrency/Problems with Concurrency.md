

## An Abstract Solution to the Concurrency Issues

We could potentially have a 'lock' of some sort that prevents other threads or programs from using or modifying the same resource while another thread or program is. 

### Critical Sections

A critical section is an abstraction that
- consists of a number of consecutive program instructions
- all code within the section executes atomically

Essentially, this is a section of code that we want to be locked and unlocked.

Critical sections are used profusely in an OS to protect data structures:
- Queues
- Shared variables
- Interrupt handlers

#### Implementations

Many ways to implement critical solutions
- Hardware vs. Software
	- some solutions require hardware support, kernel support, a combination of both, or no special support
- Multithreaded vs. Single-threaded
	- some solutions are for a single threaded application only
- Busy waiting vs. Blocking
	- in busy-waiting (spin-locks), a thread retains the CPU, and loops until it can enter the critical section
	- in blocking, a thread gives up the CPU, and waits on some queue until it gets notified that it can enter the critical section


#### Criteria for Implementations

A critical section implementation must be:
- Correct: only one thread can execute in the critical section at any given time
- Efficient: getting into and out of the critical section must be fast
- Concurrency control:  

**Implementation correctness**
1. Mutual exclusion: if a thread executes in a critical section, no other threads can be executing in that critical section (at most one thread allowed)
2. Progress: if no thread currently executes in a critical section, and there is one more thread that wishes to execute the critical section, then one of them is allowed in (at least one)
3. Bounded waiting: there is a bound on the number of times that other threads are allowed to enter the critical section after a thread has made a request to enter and before that request is granted
