## Requirements for the Course Project

Recall the [[Operating System Constraints|constraints]] there are to create the kernel in the first place.

Things with ❗ are minimum requirements. 

Unmarked or ➕ are extras/secret sauce/good to haves.

## Kernel (running on top of hardware) ❗

This *could* be a microkernel, monolithic kernel, exokernel, etc.

Needs to express **[[Problems with Concurrency|concurrency]]** in some way, create **threads**, coroutines, events, fibers, (whatever you may want to call concurrency).

The kernel should always **get out of the way quickly**. Looking for the shortest critical path for the kernel to do a task and getting out of the way.

### Maximize Parallelism ❗

Need to extract the maximum available parallelism from the system (e.g. the number of cores in the system). If you have $n$ cores and $n$ activities in the system, we should be able to run all $n$ of those activities in parallel.

#### Direct Memory Access (DMA) ❗

Extracts a lot of extra parallelism without needing to do any extra computation. You need to be able to ask I/O to write directly to a DMA buffer.

#### GPU (Secret Sauce) ➕

GPUs ensure thousands of parallel streams, and this will be something that expands the requirement. They run different tasks, so you should try to use GPU as much as possible but not necessary to do CPU tasks (etc.).

### Abstraction ❗

Some kernel applications will jump up from kernel code and run into userspace, and will need to be a user abstraction.

(e.g. a `pThread` that is exposed to the user as a wrapped format that can be used for concurrency)

### Error Handling ❗

The kernel, in its final state, should **never** panic. User processes should **not** be able to cause the system to reach a state where user processes can make the system unstable.

> [!FAQ] What about hardware issues?
> The kernel is not guaranteed to not panic if there are issues with things like hardware, power, etc. It *can* panic in those cases, but **user programs** should not be able to cause a panic.

### No Spin-Locks* ❗

Spinning means the kernel has to be blocking because it takes work away from the system. We should **not** use kernel constructs that require spin locks. In some cases, spinning is necessary (idle loops if there really is nothing to do).

\*Sometimes spin locks *are necessary* for protecting access to some resource or data structure. Doing so should be **very very brief**. The critical section should be $O(1)$.

### No Disabling Interrupts* ❗

\*Similar logic with the spin locks. There needs to be some constant amount of instructions that are run *if* disabling interrupts is necessary.

Disabling preemption is allowed for only kernel space processes, if the kernel needs to ensure interrupt-like safety. User space processes should **not** be able to do this.

### Key Decision: (Non) Preemptible Kernel ❗

A non-preemptible kernel **is** conceivable. It can be difficult, and requires making design decisions that affect how user programs are written and run. This also can affect how the system will run code.

A non-preemptible kernel requires for highly-cooperative processes in the kernel space that yield for other processes at the end of their cycles, instead of waiting for the [[Process Abstraction#Context Switching|scheduler to preempt]].

### Virtual Memory ❗

Need a very strong notion of address spaces, establish grouping between threads and address spaces.

### Processes ❗

[[Process Abstraction|Process]] needs its own context
- User ID
- Group ID
- Current Working Directory (`cwd`)
- Environment
- Open file descriptors
- Sockets
- Network connections
	- Mapped files
- Virtual address space (similar to any other OS)
- $n$-threads
	- Open-ended, but threads should allow sharing address spaces

Need to be able to create new processes. Things like `fork`/`exec` or follow your own convention. 

Need to also be able to create new threads. ❗

#### Blocking Constructs ❗

Do not force user processes to spin (e.g. give them constructs so that they can receive signals or interrupts). 

This means you need to solve race conditions that could occur between process resource contention. There are creative ways to approach this; things like `futex` in Linux ("very ugly abstraction but it works").

#### Detect Spin Locking ➕

Detect when a process is spinning and make it yield.

#### Copy-on-Write ❗

We **need** to be able to copy-on-write because doing things like forking can be very expensive. May as well share memory until we need to change anything. Then, we *incrementally* copy our memory.

This shows up in executables (you're *usually* not changing executable code), forks, dynamic linking/loading.

#### Signals ❗

Need a way to be able to handle and send signals to programs that are running on the machine. Usually very easy — essentially an interrupt but instead of hardware to kernel, it is kernel to user space.

UNIX systems have a (not-so-great) legacy system of handling signals.

### Dynamic Linking ❗

Need to have dynamic linking for shared libraries. Need them to work efficiently. 

This happens at **link time**. As such, it exists in the final executable as a reference or stub to the dynamically linked library.

➕ Preferably find a way to make sure that the shared libraries get mapped to the same addresses so the TLB doesn't need to be fully flushed. 

Additionally, we need to ensure that each process using a dynamically linked library has its **own copy** of the variables and stack and heap of the library. This ensure the processes are not able to modify other system memory.

This is a place you want to use [[Minimal Acceptable System#Copy-on-Write ❗|copy on write]].

#### Dynamic Loading ❗

User program should itself decide to load in a library during runtime, using an API from the OS similar to UNIX's `dlopen`.

