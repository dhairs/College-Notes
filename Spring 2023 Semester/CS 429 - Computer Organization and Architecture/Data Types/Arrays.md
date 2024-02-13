Implemented as a derived type (not basic)

## Syntax

Arrays are aggregates of **homogenous** scalar data (this is the reason we can do pointer arithmetic)

*Note: an array's size must be known at compile time, otherwise, you must create an array in runtime using  a call to `malloc`*.

Syntax: `T x[]` or `T x[N]` where `T` is a type and `N` is a constant-expression of integer-type and with value greater than or equal to 0.
- The type of the object `x` is "array of `T`" or "array of `N T`'s"
- The first form / type is said to have an **incomplete type** (a type that describes an object but lacks information needed to determine its size)
	- Can by **completed** by specifying size in a later declaration

**The type of an array can be *anything except* an incomplete type**.
### Example: Incomplete Type

The statement: `int x[]` is incomplete because there is no specification to it's size, we just know what the type itself is.

To complete the array, we can initialize it: `int x[] = {1, 2, 3};`

## Declaration

Syntax: `T A[N];`

This declaration reserves $L\cdot N$ contiguous bytes in memory, where $L=$`sizeof(T)` 

Remember that global variables are put into the heap, but locally scoped variables (in functions) are placed onto the stack.

`ADDR(A)` is the location of $x_A$, the address of the first byte of this contiguous chunk of space

## Arrays and Pointers

The name of an array can be referenced as an equivalent pointer variable
- E.g., after `char s[8] = "Hello!\n;`
	  `TYPE(s)` is an array-of-8-`char`s or pointer-to-`char`

## Accessing Arrays

Syntax: `A[i]`, where `i` has an integer type (*note that `C` does not check the type for you*)

`BOX(A[i])` is $[x_A+L\cdot i, x_A+L\cdot(i+1)-1]$, where:
- $x_A$ is the first byte address and
- $L$ is the length

**R-value - Right Side**  (Reading elements)
- `x = A[i]`
- Conceptually, this returns a value of the type `T` by interpreting the bits of `BOX(A[i])`

**L-value - Left Side** (Updating/Setting elements)
- `A[i] = x`
- Conceptually, this updates the value of `BOX(A[i])` with the bit representation of the right hand side of the assignment.

## Multidimensional Arrays

Syntax: `T x[M][N]`
