## Memory Dependences

Consider two memory instructions $I_{1}$ and $I_{2}$. Generally, either a load `ld <reg>, <addrmode>`, or store `st <reg>, <addrmode>`.


> [!faq] Under what conditions are these instructions dependent?
> Dependence through registers
> Dependence through memory

## Various Cases

Let EA() be a function that returns the effective address of a register.

Precondition
- $\text{EA}(I_{1})=\text{EA}(I_{2})$
- No $I_{3}$ such that $I_{1}\to I_{3}\to I_{2}$ and $\text{EA}(I_{3})=\text{EA}(I_{2})$
- Uniprocessor

### Read after Read Case

$\text{OP}(I_{1})=LD, \text{OP}(I_{2})=LD$
- We can reorder instructions
- Value from one load can be forwarded to the other load

### Write after Read

$\text{OP}(I_{1})=LD, \text{OP}(I_{2})=ST$

We cannot reorder instructions in this case.

### Read After Write

$\text{OP}(I_{1})=LD, \text{OP}(I_{2})=LD$
