# Operations on Bit Representations

Recall how we represent data in digital systems: by using [[Bits and Bit Technologies]].

## Boolean Algebra

We will work over the set of Bits: ![[Interpreting Bits#^efb035]]

We write the possible outcomes as [[Truth Tables|truth tables]]

| Not (output) | Input |
| ---- | ---- |
| **0** | 1 |
| **1** | 0 |

| And | **0** | **1** |
| ---- | ---- | ---- |
| **0** | 0 | 0 |
| **1** | 0 | 1 |

| Or | **0** | **1** |
| ---- | ---- | ---- |
| **0** | 0 | 1 |
| **1** | 1 | 1 |

| XOr | **0** | **1** |
| ---- | ---- | ---- |
| **0** | 0 | 1 |
| **1** | 1 | 0 |

## Bit Parallel Operations

Boolean operations can be extended to multi-bit quantities.

In `C`, we can write `a&b`, `a|b`, `a^b`, `~a` to perform these operations independently and in parallel on corresponding bits of these quantities.

### Ex: Given `a = 0x4a0b`, `b = 0xc3d5`

Performing `c = a & b`
	1. [[Interpreting Bits#An approach to converting bases|Convert]] `a` and `b` into binary from Hexadecimal:
		1. `a = 0100 1010 0000 1011`
		2. `b = 1100 0011 1101 0101`
	2. Now, perform the and operation, we get `c = 0100 0010 0000 0001`
	3. Can now convert this back to base 16, which is `4201`

## Bit Shifts

When shifting, you keep moving bits in the direction specified, and allow bits that overflow to just fall off and be replaced with `0`'s on the other side.

Given a $w$-bit vector $x=[x_{w-1}, \ldots, x_0]$ and an amount $k$ (with $0<k<w$), we define the following shifts:
- **Logical Left Shift**: $x<<k=[x_{w-1-k}, \ldots, x_0, 0^k]$ 
	-  **C and Java**: `x << k`
- **Logical Right Shift**: $x>>_Lk=[0^k, w_{w-1}, \ldots, x_k]$ 
	- **C**: `x >> k`
	- **Java**: `x >>> k`
- **Arithmetic Right Shift**: $x>>_Ak=[x^k_{w-1}, x_{w-1}, \ldots, x_k]$
	- **C and Java**: `x >> k`

### Ex: Given `a = 0x4a0b`, `c = 0xc3d5`

Remember by [[Interpreting Bits#An approach to converting bases|converting]],`a = 0100 1010 0000 1011`, `c (unsigned) = 1100 0011 1101 0101`

1. `b = a << 3` 
	1. Take the `a` binary representation, and shift each bit in it to the left by 3, replacing the new voids on the right with `0`'s.
	2. We get `0101 0000 0101 1000`
	3. Deconstructing that back to Hex, we get `5058`.
2. `d = c >> 2`
	1. Take the `c` binary representation, and shift each bit in it to the right by 2, replacing the new voids on the left by `0`'s. 
	2. Get the new value (not written out)
	3. Convert back to base 16: `30f5`

### Ambiguity of `>>` in C

C just lets the operating system/architecture implementation perform whatever operator it wants.

In most cases, that ends up being the arithmetic shift.

## Word Size

Memory will be abstracted as an array of $2^W$ cells, indexed from $0$ through $2^W-1$.
- Each cell holds one [[Bits and Bit Technologies#Byte|byte]] of data, each with an address.
- Memory accesses are in units of these cells (an integral number of bytes)
	- This is called "byte-addressed memory"
- The number $W$ is called the **word size** of the machine
	- This is the number of *bits* needed to hold a pointer (or address of the memory cell) on that machine
	- AArch64 and x86-64: $W=64$
	- AArch32 and IA32: $W=32$
	- This size can be smaller/vary for embedded processing units