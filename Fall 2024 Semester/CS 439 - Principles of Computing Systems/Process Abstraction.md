
## What is a Process and Process Abstraction

A process is an abstraction that supports running programs

- Different processes may run several instances of the *same* program
- In most systems, processes form a tree, with the root being the first process to be created
- At a minimum, processes require the following resources:
	- Memory to contain the program code and data
	- A set of CPU registers to support execution of the program code
- The process *may* require the other extra resources, like:
	* I/O Access

The process abstraction controls the resource access for programs.

The first process in UNIX is `init`.

### The `init` process

As the name suggests, initializes things on the machine for other processes to work, and for the OS to function properly

### Programs

A program consists of:
- `code` — machine instructions
- `data` — variables stored and manipulated in memory, classified into
	- initialized variables (globals)
	- dynamically allocated variables (`malloc`, `new`, etc.)
	- stack variables (C automatic variables, function arguments)
- dynamically linked libraries (`DLL`'s)  — libraries that were not compiled or linked with the program (contained code & data, possibly shared with other programs that use them)
- mapped files — memory segments containing variables (`mmap()`), used frequently in database programs
	- similar to DLL's, these are also not part of the program itself
	- `mmap()` takes data from the disk and maps it into memory

This is explained in further detail in [[Object Modules and Linking]].

#### Preparing Programs

![[Preparing a Program.svg]]

#### Static vs. Dynamic Linking

Why use one over the other? There are many tradeoffs, including file size, memory usage, program runtime speed, portability, etc.

|                 | Static                                                    | Dynamic                                             |
| --------------- | --------------------------------------------------------- | --------------------------------------------------- |
| **Performance** | ✅ no lookup needed to find library (negligible)           | library needs to be looked up to execute in runtime |
| **Storage Use** | libraries are included in the program file                | ✅ library doesn't need to be included with file     |
| **Memory Use**  | larger program files must be loaded into main memory      | ✅ library added to process only when needed         |
| **Portability** | ✅ machine does not have to have library as it is included | machine must have the library to run the program    |
| **Patching**    | program has to be recompiled to include patch             | ✅ program does not need to be recompiled            |

#### Running a Program

This is a multi-step process.

1. The OS creates a process with some memory allocated for it
2. The loader
	1. reads and interprets the header of the executable file
	2. sets up the process' memory to contain the code & data from the executable
	3. pushes `argc`, `argv`, `envp` onto the runtime stack
	4. sets the CPU registers properly and calls `__start()` (part of CRT0)
3. Program starts running at `__start`, which in turn calls `main()`
   We now say that the 'process' is running, no longer a 'program'
4. When `main()` returns, CRT0 calls `exit()` which destroys the process and returns all resources to the OS

### Anatomy of a Process

![[Anatomy of a Process.svg]]

### Process Life Cycle

![[The Process Life Cycle.svg]]
### Process Context

The process context consists of its address space and the CPU registers

We say that we are running the context of process $p$ if its address space is in memory and the CPU registers are used to run $p$.

#### Context Switching

The OS saves and evicts the data of the currently running process and switches to another process, setting up registers as necessary.

The `TLB` has to be flushed every time there is a context switch, which massively slows down performance.

The process implementing a program must have its own set of 'private' CPU registers
- stored in main memory

### Process Manager

The process manager has three parts:
#### Scheduler

The scheduler:
- decides who gets to run, when, and on what resources
- must:
	- improve CPU utilization (resource efficiency)
	- improve user response time (end user satisfaction)
	- be fair
- Measured by two parameters:
	- $\text{CPU utilization}=\frac{\text{time CPU is doing useful work for program}}{\text{total time elapsed}}$
	- $\text{Response time}=\text{Average}(\text{Process end time}-\text{Process start time})$

##### First Come First Served (FCFS)

Scheduler implements a FIFO queue (ready queue or run queue)

When a process becomes ready, it enters the queue

Process at the head of the queue is allowed to run ***to completion*** before bringing in the next process

Advantages:
- Simple

Disadvantage:
- Cannot give priority to more important processes
- Slower response time
- Non-preemptive FCFS can waste cycles (when waiting for I/O)

##### Shortest Job First (SJF)

Scheduler implements a queue sorted by amount of time to run the process

Process at the head of the queue is allowed to run ***to completion*** before bringing in the next process

Advantages:
- Optimal response time

Disadvantages:
- Undecidable problem to know the shortest job
	- Must ask the user predicted times
- User has to guess time
- Important processes are not necessarily given priority
- Always a shorter process, long processes will be starved

##### Preemptive vs. Non Preemptive

In non preemptive, once a process starts, it is allowed to run until it finishes
- Simple, efficient
- Creates problems
		- Infinite loops can cause queue to never move

In preemptive scheduling, a process is switched back and forth between the 'ready' and 'running' states
- More sophisticated with lots of capabilities
- Less efficient (context switching)


##### Priority-Based Scheduling

Scheduler implements a queue sorted by process' priority

Process at the head of the queue is allowed to run until:
- a **time quantum** expires, in which case the process re-enters queue, possibly getting to the queue head if it has the highest priority
- process enters the wait state, in which process is out of the queue and re-enters when the wait condition is no longer relevant

Advantages:
- Reasonable response time for high priority

Disadvantages:
- Context switching
- Subject to starvation

##### Round Robin Scheduling (RR)

Scheduler implements a FIFO queue

Process at the head of the queue runs until:
- a **time quantum** expires, in which case the process re-enters the queue
- the process enters the wait state, in which the process is out of the queue and re-enters when the wait condition is no longer relevant

Advantages:
- No process starvation
- Fair

Disadvantages:
- No context switching

##### Multi-Feedback Queues (UNIX)

The scheduler implements *several* Round Robin queues such that the processes in one queue all have the same priority.

The process at the head of the queue with the highest priority is allowed to run until:
- a **time quantum** expires, in which case the process re-enters the queue
- process enters the wait state in which the process is out of the queue and re-enters when the wait condition is no longer relevant

After running for a while, a process is relegated to the next queue in priority order (its priority is decreased).

After spending time in the I/O wait, a process is promoted to the highest priority queue (its priority is set to max).

![[UNIX Multi-Feedback Queue.svg]]

### Process Creation

The system creates the first process (`sysproc` in UNIX).

The first process creates other process such that:
- the creator is called the **parent process**
- the created is called the **child process**
- the parent/child relationships can be expressed by a process tree

Ex. in UNIX, the second process is called `init`
- it creates all the gettys (login processes) and daemons
- it should *never* die
- it controls the system configuration (num of processes, priorities, etc.)

The system interface includes a call to create processes.
- in UNIX, this is called `fork()`
	- This creates an exact copy of the current process, including all of the memory and stack
	- In order to run a different process, you must use `exec()`
- in Windows, this is called `createProcess()`

#### `exec`

#### Example

Say you have a process with process ID (PID) 0. The following code segment is executed:

```C
pid = fork();

if (pid) {
	// Parent process
} else {
	// Child process
	exec("Path name of code to be run")
}
```

The parent process