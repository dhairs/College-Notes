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

Are interested in the applications, and thus the computing system:
- Must not crash or externalize the ugly aspects of the machine
- Must protect investment in existing software and applications
- Users care about applications, not the hardware or the OS
- A good computing system is the one that is the most transparent

Contrast Windows, macOS, UNIX

### System administrator's view

