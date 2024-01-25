# Operations on Representations (Bits)

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
	3. Can now convert this into base 10, which is `4201`

## Bit Shifts

When shifting, you keep moving bits in the direction specified, and allow bits that overflow to just fall off and be replaced with `0`'s on the other side.

Given a $w$-bit vector $x=[x_{w-1}, \ldots, x_0]$ and an amount $k$ (with $0<k<w$), we define the following shifts:
- **Logical Left Shift**: `x<<k`=$[x_{w-1-k}, \ldots, x_0, 0^k]$ 