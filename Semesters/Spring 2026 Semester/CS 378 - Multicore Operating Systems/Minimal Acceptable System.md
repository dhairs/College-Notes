## Requirements for the Course Project

Recall the [[Operating System Constraints|constraints]] there are to create the kernel in the first place.

Things with ❗ are minimum requirements.

## Kernel (running on top of hardware) ❗

This *could* be a microkernel, monolithic kernel, exokernel, etc.

Needs to express **[[Problems with Concurrency|concurrency]]** in some way, create **threads**, coroutines, events, fibers, (whatever you may want to call concurrency).

### Maximize Parallelism

Need to extract the maximum available parallelism from the system (e.g. the number of cores in the system). If you have $n$ cores and $n$ activities in the system, we should be able to run all $n$ of those activities in parallel.

#### Direct Memory Access (DMA) ❗

Extracts a lot of extra parallelism without needing to do any extra computation. You need to be able to ask I/O to write directly to a DMA buffer.

#### GPU (Secret Sauce)

GPUs ensure thousands of parallel streams, and this will be something that expands the requirement. They run different tasks, so you should try to use GPU as much as possible but not necessary to do CPU tasks (etc.).

### Abstraction ❗

Some kernel applications will jump up from kernel code and run into userspace, and will need to be a user abstraction.

(e.g. a `pThread` that is exposed to the user as a wrapped format that can be used for concurrency)

### Error Handling ❗

The kernel, in its final state, should **never** panic. User processes should **not** be able to cause the system to reach a state where user processes can make the system unstable.

> [!FAQ] What about hardware issues?
> The kernel is not guaranteed to not panic if there are issues with things like hardware, power, etc. It *can* panic in those cases, but **user programs** should not be able to cause a panic.

### No Spin-Locks

Spinning means the kernel has to be blocking because it takes work away from the system. We should **not** use kernel constructs that require spin locks. In some cases, spinning is necessary (idle loops if there really is nothing to do).