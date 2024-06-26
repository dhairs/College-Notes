# Interpreting Bits

Recall the idea of Bits:
![[Bits and Bit Technologies#What is a Bit?]]

## Representations of Bits

We denote the set $\text{Bit}=\{\circ, |\}$ ^efb035

The cartesian product of $\text{Bit}$ with itself creates _bit tuples_:

- $\text{Byte}=\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}=\text{Bit}^8$
- $\text{Nibble}=\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}=\text{Bit}^4$
  - So, the nibble is $(\circ, |, |, \circ)$. Generically $(b_3, b_2, b_1, b_0)$
- We write _homogeneous_ tuples as bit vectors, using `[]` rather than `()`
  - So, we say $[\circ, |, |, \circ]$. Generically $[b_3, b_2, b_1, b_0]$
- We can also get rid of the commas and enclosing `[]`

## Shorthand Representations of Bits

- Instead of writing bit vectors, we can write $\{0,1\}$
- We create new symbols for bit vectors
  - 2 bit sequences: $\text{Quad}=\{0,1,2,3\}$
  - 3 bit sequences: $\text{Octal}=\{0,1,2,3,4,5,6,7\}$
  - 4 bit sequences: $\text{Hexadecimal}=\{0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F\}$
- Use prefix to indicate notation: `0b`, `0x`
- Use `_` to separate groups of symbols
  - E.g., `0x0000_4a6b_8192_4000`
- **Note:** you cannot use the `0b` and `_` syntax in **`C`**.

| $b_1$ | $b_0$ | Intepretation |
| ----- | ----- | ------------- |
| 0     | 0     | 0             |
| 0     | 1     | 1             |
| 1     | 0     | 2             |
| 1     | 1     | 3             |

## Specifying Interpretations

- Mappings from representations to values are called _codes_ or _interpretations_
- The most general way to specify a code is by _enumeration_ (similar to a cookbook)

Most codes we come across aren't formulaic or algorithmic, which won't work for a computer system.

We want to be able to represent our codes in a [[Value Sets|value set]].

Thats why we move to weighted codes.

## Weighted Codes

Weights represent the value of a bit at each position.

So in binary, we know bits to be $2^i$, where $i$ is the position of the bit from the left.

### Ex: How many inches in 7 yards, 2 feet, 5 inches?

We could go about this the long way, manually doing every calculation through dimensional analysis. OR, we could represent the case as a weight vector:

$\text{B}=b_{n-1}\ldots b_0$. In this case: $[7, 2, 5]$

Weights: $\text{W}=\{w_{n-1},\ldots,w_0\}$. In this case, $[36,12,1]$ (these are the number of inches in each unit, respectively)

Value: $w_0b_0+\ldots+w_{n-1}b_{n-1}=\sum^{n-1}_{i=0}w_ib_i=\text{W} \cdot \text{B}$.

### Positional Codes

If the weights can be written as a simple function of positions ($w_i=f(i)$), the function $f$ is sufficient to specify the weight vector

- Representation: $b_{n-1}\ldots b_0$, Weight: $w_i=2^i$
- Value: $\text{V}=\sum^{n-1}_{i=0}w_ib_i=\sum^{n-1}_{i=0}b_i\cdot2^i$

This gives a positional binary representation of the integer range $D=[0,2^n-1]=\{i:0\leq i\leq 2^n\}$

- This mapping is bijective
- Bit $b_i$ is said to be **less significant** than bit $b_j$ if $i<j$
- Extend this to define more significant, least significant, and most significant

### Radix-k (Base-k) Positional Codes

Generalize from binary to other bases

- Representation: $(d_{n-1}\ldots d_0)_k$ with $0\leq d_i< k$
- Weight: $w_i=k^i$
- Value: $\text{V}=\sum^{n-1}_{i=0}w_id_i=\sum^{n-1}_{i=0}d_i\cdot k^i$

## An approach to converting bases

Say we're given the number $429$ in base-10 (decimal).

How can we convert this to base-16 (hexadecimal)?

$d_2\cdot 16^2 + d_1\cdot 16 + d_0 = 429$

Just keep dividing by 16 and add the remainder's last digit.

### Base 16 to base 2

Convert each digit separately to be binary.

## Including Negative Integers

**Note:** $U_6$ represents unsigned integers using 6 bits, $S_6$ represents signed integers using 6 bits

Can we make the range of values $S_6=\{s: -32\leq s < 32\}$ rather than $U_6$?

### Two Solutions

- **Simple method**: $s=u-32$
  - Not a weighted code
  - This is called "biasing"
- **Another way**: Change the weight vector to $W_S=[-2^5, 2^4, 2^3, 2^2, 2^1, 2^0]$
  - This is called the "two's complement" representation

## Range Expansion

Given a $w$-bit vector $b=[b_{w-1}, \ldots, b_0]$, we want to _expand_ it to a $(w+k$)-bit vector $b'$ and _re-interpret_ $b'$ as an integer.

- Moving from a smaller $w$-bit wheel to a larger $(w+k)$-bit wheel

### Expansion:

- Unsigned: $b'=[0^k, b_{w-1}, \ldots, b_0]$
- Signed: $b'=[b^k_{w-1}, b_{w-1},\ldots, b_0]$

### Re-interpretation: $b$ and $b'$ represent the same integer

- Unsigned: proof is obvious
- Signed: proof by induction, $k=1$ is the base case, divide it into two cases based on the value of $b_{w-1}$

## Range Truncation

Given a $w$-bit vector $b=[b_{w-1},\ldots, b_0]$, we want to _truncate_ it to a $k$-bit vector $b'$ where $0<k<w$ and _re-interpret_ $b'$ as an integer

- Moving from a larger $w$-bit wheel to a smaller $k$-bit wheel

### Truncation: $b'=[b_{k-1},\ldots,b_0]$

### Re-interpretation:

- Unsigned: if $b$ represents $n$, then $b'$ represents $m=n\;\text{mod}\;2^k$
- Signed: if $b$ represents $n$, then $b'$ represents $m'$, where $m'$ has the same representation on the signed $k$-bit wheel as $m$ does on the _unsigned_ $k$-bit wheel.

To understand this, lets look at a few calculations

### Remainder and Modulus

Given an integer $a$ and non-zero integer $d$:

- $\exists q, r: a=qd+r, 0\leq r < |d|$
- We write $r=a\;\text{mod}\;d$. $r$ is also non-negative

### Special Bit Operations

Because we express bits as $2^i$ in binary, we can do special operations with them. Often called bitwise operations. There are many [[Operations on Representations]] to look over.
