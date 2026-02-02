## Thread Private Data

`x86` and `ARMv8` both have methods for providing private data to a thread. Threads in general need to be able to store some private data — usually in some notion of a stack.

`x86` has the `fsbase` register that is unique to a thread (outside of the traditional general purpose registers \[GPRs\]). 

`AArch64` defines `R18` as a **platform register**. The platform tells the compiler what to do with this register.

These registers point to the thread control block (or whatever in the kernel defines what is unique to that thread).

### x86

x86 address translation involves two-step, which affects the `fsbase`. 

Traditionally, [[Paging|paging]] takes a virtual address and produces a physical address. However, on x86, there is first the **segmentation** step. The instruction being run produces an **effective address (EA)**.

#### Effective Addresses (EA)

Take on the form of $\text{displacment} +\underbrace{(\text{base},}_{\mathbb{R}} \underbrace{\text{index},}_{\mathbb{R}} \underbrace{\text{scale}}_{\{1, 2, 4, 8\}})$.

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
