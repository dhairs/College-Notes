# Interpreting Bits

Recall the idea of Bits:
![[Bits and Bit Technologies#What is a Bit?]]

## Representations of Bits

Therefore, we can denote the set $\text{Bit}=\{\circ, |\}$

The cartesian product of $\text{Bit}$ with itself creates *bit tuples*:
- $\text{Byte}=\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}=\text{Bit}^8$ 
- $\text{Nibble}=\text{Bit}\times\text{Bit}\times\text{Bit}\times\text{Bit}=\text{Bit}^4$ 
	- So, the nibble is $(\circ, |, |, \circ)$. Generically $(b_3, b_2, b_1, b_0)$
- We write *homogeneous* tuples as bit vectors, using `[]` rather than `()`
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
| ---- | ---- | ---- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 2 |
| 1 | 1 | 3 |

## Specifying Interpretations

- Mappings from representations to values are called *codes* or *interpretations*
- The most general way to specify a code is by *enumeration* (similar to a cookbook)

Most codes we come across aren't formulaic or algorithmic, which won't work for a computer system.

Thats why we move to weighted codes.

## Weighted Codes
