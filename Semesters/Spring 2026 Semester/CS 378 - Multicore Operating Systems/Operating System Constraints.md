## Design Constraints

### Architecture Support
- Any architecture, we get to choose
	- 64-bit is standard
- x86, ARM, RISCV, MIPS, SPARQ, POWERPC, etc.
- Don't need to pick and know what arch to support from the start
	- Can be changed

### Platform

Need to pick platform being run on in addition to the architecture. (e.g. Raspberry Pi for ARM).

RPi3/4 may require implementing a USB specification to be able to access networking. 
- Could always take a look at Linux's USB driver to find out how to do it

It IS okay to find other drivers online and make them work here (need to have it cleared by the professor AND MARK it).

### Hardware or Emulation

Using emulators is useful for development and quick turnaround in testing. (QEMU is the standard for the most part).

Need to run on hardware in a meaningful way to be able to get an A in this course.

### Kernel Implementation

### Pick a Language

- C
- **Rust** - many reasons to want to use Rust
	- Bugs are costly in operating systems
	- Would be nice to prove properties of the system, like bounds checking, memory safety, ownership, correctness, etc.
	- *Some* sense of formal verification
	- [Verus](https://github.com/verus-lang/verus) can prove correctness of parts of the system for Rust
- C++
- Zig
- Nim
- Odin
- etc.

Minimal architecture-specific assembly

### Design of Kernel

Generally, hardware is very simple in terms of abilities. You can usually manage some memory, use I/O, and that's about it. 

On top of that, we build the kernel that abstracts much of the hardware away from the end user. [[Process Abstraction]] abstracts away things like [[Virtual Addresses|Virtual Memory]] and the [[Flat File Systems|Filesystem]], Networking, etc.

Then, even past that, we might even have a hypervisor running **below** the kernel. The hypervisor could also abstract hardware out and make the kernel think it's running directly on the hardware. That way, you can use multiple kernels on the same hardware.

On top of the kernel we have the userland. Lots of virtual processes and applications that are under the idea that they are accessing hardware directly.


> [!faq]+ What if the userland process is an emulator
> It becomes recursive. You could have your own emulation for hardware onto that, and then could also add hypervisors, kernels, etc. on top of it. 

### System Calls

Because user applications cannot go to hardware directly, they need to talk through the kernel using system calls. Depending on the nature of the hypervisor and kernel, they sometimes run on the hardware. Meaning, user applications *can* directly use the hardware in **some** ways, but not all. The kernel can use it in **more** ways, and the hypervisor can access **even more**. Essentially, parts of the OS abstract and mask away parts of the hardware.