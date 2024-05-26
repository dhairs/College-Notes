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

## Casting Pointers

Casting the type of a pointer changes the type but *not* the value

This means when we cast the type of a pointer, we change the `sizeof` of it, because it is interpreted as whatever the new type is.

## Pointers to Functions

(Function Pointers)

Function types are just another derived type in `C`, so we can have pointers to them

For a function object `f`, `ADDR(f)` is simply the memory address to where its code starts. 

*Note that in C you cannot use `sizeof` on a function*

To set a pointer, no need to use the unary `&` for the address, you can simply set `fp = fun` and it would set `fp` to the pointer.

When calling a function pointer, you just call it as usual, no need to de-reference.
### Example

Say we declare:

```c
// example.h

int fun(int x, int *p); // a function that takes in an int and int pointer and returns an int
int (*fp) (int, int*); // a pointer to a function that takes in an int and an int pointer and returns an int
int y = 1;
```

`TYPE(fun): int & int ptr -> int` 
`TYPE(fp): (int & int ptr -> int)ptr`
