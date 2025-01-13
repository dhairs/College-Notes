
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
- context switching

##### Multi-Feedback Queues (MFQ) (UNIX)

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
	- This creates an exact copy of the current process, including all of the memory (heap, stack, etc.) and pointers (this is copying the page tables for the process)
	- In order to run a different process, you must use `exec()`
- in Windows, this is called `createProcess()`

Because of address spaces, pointers and heaps retain the same values but in reality have different contexts and do not affect each other.

#### `fork`

Parent and child's code must be in the same program
- limits the usefulness for general purpose process creation
- gets out of control quickly if many children are to be created

The child inherits all the open files and network connections
- having parent and child share the I/O and network is very tricky
- behavior with respect to the network connections varies
- if the child does not use the inherited open files, then the work to set up the sharing is useless and the resources that are consumed within the OS are for no reason

Using `fork` is **expensive**.

There is an alternative that does not fully copy the process memory, called `vfork` that does *not* copy the page tables for the parent process.

#### `exec`

The `exec()` call allows a process to 'load' a different program and start execution at `__start`

It allows a process to specify the number of arguments (`argc`) and the string argument array (`argv`)

If the call is successful:
- it is the same process
- it runs a different process

Two implementation options:
1. overwrite current memory segments with the new values
2. allocate new memory segments, load them with the new values, and deallocate old segments

If we are overwriting current memory and there is an error in the `exec` and overwriting, we have a problem, because the memory is now partially overwritten. As such, it is better to go with the 2nd option and ensure that the new program is able to run.

`exec` replaces the entire memory of the current process with a new program that is provided by pathname. A call to `exec` should *not* return if it is successful. 

This system call may cause confusion because it may be fair to ask "how is the parent getting the return value of the process if `exec` isn't supposed to return anything?"

This works because `exec` replaces the process with a different program. Then, this process is **still the child** of whatever process called `fork` to create it, but there is no longer the old program running, it is a new program, which means that the process return value will be the return value that the parent is able to read.

##### Example of `exec`

```C
pid = fork();

if (pid) {
	// Parent stuff
	rval = wait(pid);
	printf("%i", rval)
} else {
	err = exec("/path/to/some/file");
	printf("%i", err);
}
```

Let's say that the file `/path/to/some/file` exists and `exec` successfully executes. The print statement is never called. Now, the parent process is in the first block of the `if` statement, and is waiting for the result of the child process. When the child process exits, the parent will print the return value (exit code). 

Lets say that the file `/path/to/some/file` does not exist and `exec` fails. `exec` will return a value and `err` will have a value. There will be something printed to the console.

#### The `fork`/`exec` sequence

#### Example

Say you have a process with process ID (PID) 0. The following code segment is executed:

```C
int i = 3;
pid = fork();

if (pid) {
	// Parent process
	i++;
} else {
	// Child process
	i++;
	exec("Path name of code to be run")
}
```

`i = 4` in both copies when the process is ended.

The reason the `if` statement works above is because when the process is forked, the new PID is assigned to the PID variable only in the parent process **because** it only assigns the variable **after** the fork, so the copy that the child process has is uninitialized and equal to `0`.


#### Example with Files

Files connections are copied over along with the rest of the data when using `fork`, so in the following code segment, both the child and parent are accessing and editing the same file:

```C
fopen(...)
pid = fork();

if (pid) {
	// Parent process
	i++;
	fwrite(...)
} else {
	// Child process
	i++;
	fwrite(...)
}
```

This will lead to a race condition, because we don't know which process will edit the file first. This is **not deterministic**.

### Process Termination

#### Orderly Termination: `exit()`

After the program finishes execution, it calls `exit()`

The system call does the following:
- takes the "result" of the program as an argument (CRT0 calls `exit()` with the value returned by the main program)
- closes all open files, connections, etc.
- deallocates memory
- deallocates most of the OS data structures supporting the process
- checks if the parent is alive:
	- if so, it holds the result value until the parent requests it, process doesn't really *die*, but enters the **zombie/defunct** state
	- if not, deallocates all data structures, the process is now dead
- cleans up all waiting zombies

##### `wait`

The `wait` system call allows a parent process to wait for a child process's return value. The thread waits until the child process is exited.

### Process Control

The OS must include calls to enable special control of a process:
- Priority manipulation
	- `nice()` which specifies the base process priority (the initial priority)
	- recall that UNIX priority decays as the process consumes CPU
- Debugging support:
	- `ptrace()`, allows a process to be put under control of another
	- the other process can set breakpoints, examine registers, etc.
- Alarms and time:
	- sleep puts a process on a timer queue waiting for some number of seconds, supporting an alarm functionality

#### Signaling

the OS translates some events into **asynchronous** signals:
- input/output
- alarms

The OS also translates exceptions into signals:
- e.g. memory access violations, illegal instructions, overflow, etc.

Signals also used for process control:
- e.g. `SIGKILL` to kill a process, `SIGSTOP` to stop a process, etc.

Rudimentary process communications:
- e.g. process may use the `kill()` system call to send signals to each other (`SIGUSR1`, `SIGUSR2`)

#### Signal Handling

A process can:
- rely on the default signal handler (e.g. core dump in UNIX)
- ignore signal (temporarily or permanently)
- 

### Basic Process Implementation

Each process has a **process control block** (PCB) that: