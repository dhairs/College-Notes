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
	- `return ((x^y) & 0x80808080) ^ s` - we know the bottom 7 bits are good, so we can bring down those values using the XOR mask with 0s, because `x | 0 = x`

## Shifting

Shifting quantities to bring certain bits into desired positions, typically used in conjunction with masking.

**Examples**:
- Extract the `Most Significant Byte` of `x`
	- `return (x >> ((sizeof(int) - 1) << 3)) & 0xFFU;`
	- Rotate (not "shift") `x` left by `k` positions
		- `return (x << k) | (x >> ((sizeof(int) << 3) - k));` - need to make sure `x` is unsigned

## Recursive Doubling

General and powerful primitive for parallel algorithm design (parallel sum/reduction or prefix sum/scan)

Divide and Conquer Strategy:
1. Breaks up word into two equal-sized independent pieces — think of merge sort.
2. Works on them in parallel
3. Combines their results using an *associative* operator

Allows us to reduce the step complexity of algorithms from $O(n)$ to $O(\log_2(n))$

**Examples**:
- Counting the number of 1-bits in an `unsigned int x`

```c
int POPCNT(unsigned x) {
	x = (x & 0x55555555) + ((x >> 1) & 0x55555555);
	x = (x & 0x33333333) + ((x >> 2) & 0x33333333);
	x = (x & 0x0F0F0F0F) + ((x >> 4) & 0x0F0F0F0F);
	x = (x & 0x00FF00FF) + ((x >> 8) & 0x00FF00FF);
	x = (x & 0x0000FFFF) + ((x >> 16) & 0x0000FFFF);
	return x & 0x0000003F;
}
```

- Counting the parity of `int x`

```c
int PARITY(int x) {
	int y = x ^ (x >> 1);
	y ^= (y >> 2); y ^= (y >> 4);
	y ^= (y >> 8); y ^= (y >> 16);
	return y & 0x1;
}
```

- Counting the number of leading zeros in an `unsigned int x`

```c
int NLZ(unsigned x) {
	x |= (x >> 1); x |= (x >> 2);
	x |= (x >> 4); x |= (x >> 8);
	x |= (x >> 16);
	return POPCNT(~x);
}
```

## Structured Permutations

Moving all the bits in a structured manner (reversal, perfect shuffle, etc.) can be accomplished using a logarithmic number of steps.

Used recursive doubling principles.

Used for: design of interconnection networks, Fourier analysis, cryptography, etc.

**Examples**:
- Bit reversal of an `unsigned int x`

```c
unsigned BitReversal(unsigned x) {
	x = (x & 0x55555555) << 1 | (x & 0xAAAAAAAA) >> 1;
	x = (x & 0x33333333) << 2 | (x & 0xCCCCCCCC) >> 2;
	x = (x & 0x0F0F0F0F) << 4 | (x & 0xF0F0F0F0) >> 4;
	x = (x & 0x00FF00FF) << 8 | (x & 0xFF00FF00) >> 8;
	x = (x & 0x0000FFFF) << 16 | (x & 0xFFFF0000) >> 16;
	return x;
}
```

- "Outer perfect shuffle" of the bits of an `unsigned int x`

```c
unsigned OuterPerfectShuffle(unsigned x) {
	x = (x & 0x0000FF00) << 8 | (x >> 8) & 0x0000FF00 | x & 0xFF0000FF;  
	x = (x & 0x00F000F0) << 4 | (x >> 4) & 0x00F000F0 | x & 0xF00FF00F;  
	x = (x & 0x0C0C0C0C) << 2 | (x >> 2) & 0x0C0C0C0C | x & 0xC3C3C3C3;  
	x = (x & 0x22222222) << 1 | (x >> 1) & 0x22222222 | x & 0x99999999;  
	return x;  
}
```

## Lookup Tables

Keep precomputed values in a lookup table.

Used standalone or as an assist to other methods

Must control size of lookup table.

**Examples**:
- Alternative version of `POPCNT(x)`, uses `C` preprocessor to avoid writing out table manually

☠️ Code, don't ever try to write this type of code without knowing how it works

```c
static const char table[256] = {  
	#define B2(n) n, n+1, n+1, n+2  
	#define B4(n) B2(n), B2(n+1), B2(n+1), B2(n+2)  
	#define B6(n) B4(n), B4(n+1), B4(n+1), B4(n+2)  
	B6(0), B6(1), B6(1), B6(2)
};

int POPCNT2(unsigned x) {  
	return table[x & 0xFF] +  
	table[(x >> 8) & 0xFF] +  
	table[(x >> 16) & 0xFF] +  
	table[(x >> 24)];  
}
```
