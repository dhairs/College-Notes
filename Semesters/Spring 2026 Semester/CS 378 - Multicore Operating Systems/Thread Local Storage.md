## Thread Private Data

`x86` and `ARMv8` both have methods for providing private data to a thread. Threads in general need to be able to store some private data — usually in some notion of a stack.

`x86` has the `fsbase` register that is unique to a thread (outside of the traditional general purpose registers \[GPRs\]). 

`AArch64` defines `R18` as a **platform register**. The platform tells the compiler what to do with this register.

These registers point to the thread control block (TCB) (or whatever in the kernel defines what is unique to that thread).

### x86

x86 address translation involves two-step, which affects the `fsbase`. 

Traditionally, [[Paging|paging]] takes a virtual address and produces a physical address. However, on x86, there is first the **segmentation** step. The instruction being run produces an **effective address (EA)**.

#### Effective Address (EA)

Take on the form of $\text{displacment} +(\underbrace{\text{base}}_{\mathbb{R}}, \underbrace{\text{index}}_{\mathbb{R}}, \underbrace{\text{scale}}_{\{1, 2, 4, 8\}})$.

Then, we can also add the segment register `seg_base`:

$$\underbrace{\text{seg\_base}}_{\text{Segment Context}} + \underbrace{(\text{base} + \text{index} \times \text{scale} + \text{disp})}_{\text{Effective Address (EA)}}$$

We can then generate a translation using:

$$\text{Effective Address} = \text{base} + \text{disp} + (\text{index} \times \text{scale})$$
$$
\begin{align}
\text{Linear Address} = \text{seg\_base} + \text{base} + (\text{index} \times \text{scale}) + \text{disp} \\
\text{Linear Address}=\text{seg\_base} +\text{Effective Address}
\end{align}
$$


The segment register also contains a limit that is enforced by hardware.

The `gs` register is only 16 bits but we want 64 bit offsets. As a result, there is another register called `fsbase` and instructions `wrfsbase` and `rdfsbase`.

#### In Software

We should create some sort of structure (like a TCB) and then update the `fsbase` to point to the TCB.

Thread local variables need to be accessed with `fsbase`.

In C/C++/Rust, we have the `thread_local` specifier that defines that each thread will have this data.

## ELF Format

In the elf format, there is a `PT_TLS` segment that defines the thread local storage variables. The symbol table will mark variable `x` as `tls` and will generate an additional field defined as `xoff` (or something similar) to tell you where that variable is within the `PT_TLS` segment.

The `fsbase` or `r18` is used to access the TCB, which points to itself (enforced). Then, the offset is applied to the thread control block as a negative offset. This means that if the thread control block is "under" the `fsbase` address, the thread local variables are "above" the `fsbase` address, and vice-versa. 

This structure above the TCB needs to be allocated by the kernel at load-time. It must be the size of the `PT_TLS` segment of the loaded file.

## `gsbase`

The `gsbase` register is often used by the kernel to manage data specific to a core (like core number, running thread, etc.). The user space can define its own use case for the register as well. 

*e.g.* in Windows, `GSBASE` is used for thread local storage.