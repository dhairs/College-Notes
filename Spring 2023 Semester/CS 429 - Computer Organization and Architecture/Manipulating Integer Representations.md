## Sizes of Integer Types

The system header file `<limits.h>` defines several macros that expand to various limits and parameters of the standard integer types. Basically, each machine has its limits set globally on the standard `C` lib.

## Bit Parallel Operations

Anything you can do one a single bit, you can extend to do with 32 bits in parallel.

The key idea is to use the bitwise extensions of `&`, `|`, and `~` along with identities from Boolean algebra.

**Examples**:
- Compute `x&y` using only `~` and `|`: `return ~(~x|~y)`
- Swap variables `x` and `y` without using a temporary: `x ^= y ^= x ^ = y`
	- Same thing as: 
		- `x ^= y;`
		- `y ^= x;`
		- `x ^= y;`

Remember how XOR works:

| **x, y** | **0** | **1** |
| ---- | ---- | ---- |
| **0** | 0 | 1 |
| **1** | 1 | 0 |

## Masking

The boolean identities `x & 1 = x` and `x | 0 = x`

The trick is to generate masks efficiently and portably

**Examples**:
- Extract the `Least Significant Byte` of `x`
	- Perform `&` of `x` with `OxFFU`: `return x & 0xFFU`
		- `OxFF` is `1111 1111` in binary, when doing the and, extra `0`'s are appended to the left as needed.
- Add corresponding bytes of `x` and `y`
	- `s = (x & 0x7F7F7F7F) + (y & 0x7F7F7F7F);` - we are getting rid of the most significant bit in the byte, so if there does happen to be a carry, all we get is a 1 there
	- `return ((x^y) & 0x80808080) ^ s`