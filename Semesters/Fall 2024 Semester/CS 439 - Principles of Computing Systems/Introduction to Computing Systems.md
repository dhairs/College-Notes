## Types of Computing Systems

**Desktops/laptops:** Windows, Linux, macOS
**Servers**: Windows, Linux, Proprietary UNIX systems, HPUX, AIX, Solaris, CMS/MVS
**Embedded & Mobile**: QNX, OS-9, VxWorks, Lynx, PalmOS, Windows CE, BlackberryOS, Android, iOS, HarmonyOS

## The 5 Views of a Computing System

Your view of a computing system is dependent on who you are.

1. Hardware view
2. Operating system designer's view
3. Application programmer's view
4. End-user's view
5. System administrator's view


### Hardware View

The hardware designer interacts with software at a very low level, often working with:
- The boot process
- Devices and how the software can use them
- The interactions between hardware and software
	- What feature to add to enhance the performance and utility of software
		- E.g.,: Trusted Execution Environment (TEE) (too slow, an overstepping of hardware design)

### Operating system designer's view

The interest revolves around the OS itself, its internal structure, its efficiency, performance, data structures, etc.

OS designers often ask questions like:
- How can we make the OS more efficient
- How can we add more functionality
- How do we debug the OS?
- How do we make it more reliable, scalable, secure, etc.

### Application programmer's view

The programmer perceives the system as a programming language environment with a library with a well-defined set of API's.

They are often concerned with:
- What abstractions are available from the PS?
- How well is the API structured? Not too low-level, or high-level
- How portable is the interface?
- Protection of the intellectual investment — don't want to keep rewriting the same program for each new hardware or OS release.

This explains why Windows has been so successful.

### End-user's view

Interested in the applications, and thus the computing system:
- Must not crash or externalize the ugly aspects of the machine
- Must protect investment in existing software and applications
- Users care about applications, not the hardware or the OS
- A good computing system is the one that is the most transparent

Contrast Windows, macOS, UNIX

### System administrator's view

Interested in managing the computing system:
- How can it track usage for accounting?
- How easy is it to install new software? Upgrades?
- Security
- Fairness
- Reliability

Contrast Windows, macOS, UNIX, and mainframe systems.

### Conflicts Between Views

There are often some disagreements or issues that arise between different views, for example:
- Hardware vs. OS designer
- API vs. User
- API vs. OS designer (having to stick to an API that's worse)
- User vs. System administrator

## Operating Systems

The operating system (OS) is a program that mediates between the application programs and the hardware

It provides abstractions to simplify building applications:
- files instead of 'bytes on a disk'
- contiguous memory regions instead of 'bits in a RAM chip'
- processes to run applications

It also allows application programs to co-exist peacefully:
- enforces security policies
- enforces safety measures
	- E.g., virtual memory

Allows effective usage of hardware resources 
- E.g., CPU time scheduling

### Hardware Support

The operating system needs to:
- Control I/O devices 
- Control application access to the hardware

It needs to do all this while denying these privileges to user programs for protection and abstraction/ease of use.

The hardware supports two modes of operation (or more):
- Access to hardware and I/O devices is done through privileged instructions, only available in **supervisor mode**
- Privileged instructions cannot be executed in **user mode**
	- this is where applications are run
	- UNIX terminates the application when it attempts to execute a privileged instruction

This means the OS also manages main memory. The OS also manages what *mode* the system is in.

### Implementation of Machine Modes

There are a few ways to do have the machine store state on what mode it is in:
- Using a bit in the processor to signify mode 
- Using protection “rings”
	- innermost ring has the most privilege, and moving outwards reduces privileges until the outermost ring, with user privilege.
- Operating system code runs in the supervisor mode while user programs run in user mode
- Switching from user to supervisor mode occur on:
	- **interrupts (async)**: hardware devices needing service
		- store machine state deal with interrupt, then return back to previous machine state
	- **exceptions**: user program acts silly, errors out
	- **trap instructions**: user program requires OS service (e.g., system call)
	- processor state is saved in all of these instances
- Switching back to user mode occurs by an `RTI` instruction


### Interrupt Handling

1. The hardware calls the operating system at a predefined location
2. The operating system saves the state if the user program
3. The operating system identifies the device and the cause of the interrupt
4. The OS responds to the interrupt (ex. Killing the program with `CTRL + C`)


### Exception Handling

1. Hardware calls OS at predefined location
2. OS determines the cause of the exception
3. If the user program has an exception handler, the OS adjusts

### System Calls

1. User program calls the trap instruction


### Implications of OS Structure

The OS is just a program:
- it has a `main()` function, which gets called only once (during boot)
- like any program, it consumes resource, like memory, can do silly things (like generating an exception), etc.

It’s a strange program, because:
- it is entered from different locations in response to external events (ex. Interrupts)
- it does not have a single thread of control: it can be invoked simultaneously by two different events (e.g., system call and interrupt)
- It is not *supposed* to terminate
- It can execute any instruction in the machine

Hardware generates exceptions, so a raised exception will cause the OS to terminate itself.

### Control Flow 

![[OS Control Flow.svg]]
