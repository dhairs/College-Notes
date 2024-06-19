## About

Implemented as a derived type (not basic)

What is the difference between Structs and [Arrays](Arrays.md)? **Struct**'s are heterogenous. 
- can also be called a `record`
- objects being aggregated are called the `fields`
## Syntax

**Anonymous Structure**:
`struct {...} x;`

**Tagged Structure (`T` is the tag)**
`struct T {...} x;`

You need to use a tagged structure if you want to refer to the same type within the struct itself (e.g., a Linked List node with a field pointing to the next node of the same type)

`typedef struct {...} T` can be used to define a shorthand synonym for the structure type.

## Declaration

The declaration `struct T {...} x` has the following effect:
- Reserves `sizeof(struct T)` contiguous bytes in memory to hold variable `x`, starting at some location $M_x$ (*thus, `SIZE(x) = sizeof(struct T)`*)
- `ADDR(x)`$=M_x$ 

Fields of the structure appear **in the same order** in memory as the declaration
- Each field `f` of the object `x` has a type of $T_f$ and an offset $o \geq 0$ such that the field `x.f` occupies `sizeof(`$T_f$`)` bytes starting at memory location $M_x+o$ 

The size of the struct is **greater than or equal to** the sum of the sizes of all it's fields.

Why greater than?

## Accessing

Given `struct T{...} x, *xp;`

Syntax: `x.f` or `xp->f`

### R-Value

Returns a value of type TYPE(`x.f`) by interpreting the bit representation in BOX(`x.f`)

### L-Value

Updates memory bytes of BOX(`x.f`) with the type-appropriate bit representation of the **R-value** of the assignment operation. (like setting a variable)

