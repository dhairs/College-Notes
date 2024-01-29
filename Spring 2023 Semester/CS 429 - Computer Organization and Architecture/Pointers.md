## What are Pointers

Essentially, a pointer is an *address* to memory on your machine. 

The space taken up by a pointer is determined by your machine's [[Operations on Representations#Word Size|word size]].

Think of your memory as an array: 

Lets say we have 

```c 
int b = 6;
int *c = &b
```

This means **b** is a reference to the `6` in memory, as shown below. `*c` denotes a pointer to the **address** of b (that's what the `&` operator denotes.) As a result, `b` is pointing to that `6` in the memory, and `*c` is the address of that `6` in memory.

| - | - | `6` | - |
| ---- | ---- | ---- | ---- |
| - | - |  - | - |

### Segmentation Faults

These occur when the code is unable to access a memory location specified in the program runtime. This can occur because the memory address doesn't exists or if the program doesn't have permission to read that memory address.