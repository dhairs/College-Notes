

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

#### Disabling Interrupts

For a single threaded system, interrupts are the only source of concurrency problems (hardware or software).

It follows that a simple solution to implement a critical section is: 
- disable interrupts at the beginning of the critical section
- enable interrupts at the end of the critical section

For OS's, disabling hardware interrupts is very dangerous
- Can lead to delaying response to an important event
- Does not scale well in multiprocessor environments with a shared bus

### Synchronization Instructions

Relying on test-and-set instructions
- implemented in hardware
- is a machine instruction that:
	- reads a value from memory
	- tests the value against some constant
	- if the test is true, it sets the value in memory to a different value
	- reports the result of the test in a flag (usually carry or zero flag)

This instruction executes atomically.
- it locks the memory bus while executing
- does not scale very well in multiprocessor environments with a shared bus

### Blocking Synchronization

There are a few types of blocking synchronization systems:
- [[Semaphores]]
- Monitors
- Condition Regions