## Representation and Multiplication

Recall how [[Floating Point Numbers]] are [[Floating Point Numbers#Choice 2 Floating Point|represented]].

$x\in FP(p,q;b),x\text{ normalized}$
- Precision $p$
- Exponent width $q$
- Base $b$
- Hidden bit for $b = 2$

Let $x=(-1)^n\times s\times b^e$.

Then $x_{1} \otimes x_{2}=\text{ROUND}(x_{1}\times x_{2})$

For $b = 2$,

$$
((-1)^{n_{1}} \otimes s_{1} \otimes 2^{e_{1}}) \otimes ((-1)^{n_{2}} \otimes s_{2} \otimes 2^{e_{2}})=\text{ROUND}(\text{NORM}((-1)^{n_{1}+n_{2}}\times(s_{1}\times s_{2})\times 2^{e_{1}+e_{2}}))
$$

### Multiplication Algorithm

Multiple significands (including the hidden bit). 
We need to multiply unsigned integers. 
Add exponents (handling bias). 
Determine sign bit, easy logic block. 
If product is 0, adjust representation.

Normalize product
- Significand too big: shift right, increase exponent
- Significand too small: shift left, decrease exponent

If exponent over or under-flows, generate exception.

Round to appropriate number of bits
- May need renormalization


### Rounding and Normalization

Three pieces of data enough to produce the correctly rounded value:
- Rounding digit $r$
- Sticky digit $s$, anything that happens after rounding error point.
- Guard digit $g$

#### Example

(*Note*: this was generated with NotebookLM using my notes, may be prone to error)

Let's walk through an example of floating-point multiplication using a shift-and-add multiplier with a **7-bit mantissa** (including the hidden bit). We'll focus on the significand multiplication, normalization, and rounding steps.

Assume we are multiplying two normalized floating-point numbers:

- $X = (-1)^{s_1} \times 1.01101 \times 2^{E1}$
- $Y = (-1)^{s_2} \times 1.10100 \times 2^{E2}$

Here, the significands are $1.01101$ and $1.10100$. For simplicity, we will perform unsigned multiplication.

**1. Multiply Significands (7-bit x 7-bit unsigned multiplication)**

We are multiplying $101101$ and $110100$ (binary), which are the bit representations of the significands without the binary point. We will use the shift-and-add method:

|Step|Multiplier Bit|Accumulator|Operation|
|:--|:--|:--|:--|
|0||00000000000000|Initialize|
|1|0|00000000000000|Shift|
|2|0|00000000000000|Shift|
|3|1|00010110100000|Add, Shift|
|4|0|00010110100000|Shift|
|5|1|01000100100000|Add, Shift|
|6|1|10010110100000|Add, Shift|

The result of the multiplication is $10010110100000_2$.

**2. Normalization**

The binary point is assumed to be after the first bit of the significand (hidden bit). So we rewrite the result as $10.010110100000$. Since the number is greater than 2, we shift right and increase the exponent:

$1.0010110100000 \times 2^1$

Now we have a normalized form.

**3. Rounding**

We need to round to 6 bits after the hidden bit (since the hidden bit is not explicitly stored). So we need to truncate or round $1.0010110100000$ to $1.00101x$. We consider the guard ($g$), round ($r$), and sticky ($s$) bits.

- Our number is $1.00101 \textbf{1}0100000$
- Rounding digit ($r$) is 1
- Guard digit ($g$) is 1
- Sticky digit ($s$) is 0 (since there are no more non-zero digits)

Using round-to-nearest, since the round bit is 1, we round up. $1.00101 + 0.00001 = 1.00110$

**4. Final Result**

The final significand after multiplication, normalization, and rounding is $1.00110$. The complete result would be:

$(-1)^{s_1+s_2} \times 1.00110 \times 2^{E1+E2+1}$, where:

- $s_1 + s_2$ determines the sign of the result.
- $E1 + E2 + 1$ is the biased exponent, with "+1" resulting from the normalization shift.

This example illustrates the basic steps involved in floating-point multiplication using a shift-and-add multiplier.

## Floating Point Multiplier Design

Input:
- Two [[Floating Point Numbers#Normalized FP Numbers|normalized]] floating point number $x$ and $y$

Outputs:
- $p=\text{ROUND}(x\cdot y)$
- $\text{Err}=\text{Error Flag}$

![[FP Multiplier.svg]]

### Shift and Add Multiplier

When the state machine is at state ST'/0, all outputs are 0, and the machine is waiting for start signal.

