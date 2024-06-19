## The Design Problem

With 64-bit integers, we only get `18,446,744,073,709,600,000` distinct values. But quantities in physics and mathematics can easily go well beyond this.

We need to find something that is not only efficient in storage space, but also in computational time, because we only have so many resources.

![[Floating Point Design Problem.svg]]

## Choice 1: Fixed Point

Represent a number $x$ as $\pm x_i * x_f$ where:

- $x_i$ is the integer part of $x$, represented using $a$ radix-$k$ digits
- $x_f$ is the fractional part of $x$, represented using $b$ radix-$k$ digits

Represent $x$ as a $(1+a+b)$ digit radix-$k$ string that we write from most-significant to least-significant digit at the triple (sign; the $a$ digits of $x_i$; the $b$ digits of $x_f$)

Thus, in a fixed point system with ($k=2,a=5,b=16$):

- The value $\frac{11}{2}$ would be represented as (1; 000 0000 0000 0101; 1000 0000 0000 0000), or `0x80058000`
- The value $\frac{1}{10}$ would be represented as (0; 000 0000 0000 0000; 0001 1001 1001 1001) or `0x00001999` (approximate)
- The range would be $2^{-16}\leq |x| \leq 2^15-\epsilon$ along with $\pm0$

The problem with this method is there are a lot of wasted bits, we don't use them properly.

For this reason, we move to using Choice 2:

## Choice 2: Floating Point

Extend the idea that is used in scientific notation:

- Represent $x$ as $\pm S\times 10^E$ with $S=(d_0\cdot d_1 \ldots)_{10}$ where $1\leq d_0 < 10$
- $S$: significant/mantissa; $E$: exponent
- The representation of the value $\frac{11}{2}$ is uniquely $+5.5\times 10^0$

Why?

### From Base-10 to Base-2

Represent $x$ as $\pm S\times 2^E$ with $S=(b_0\cdot b_1 \ldots)_{2}$ where $1\leq b_0 < 2$

- Not an infinite number of bits after binary point, so $S=(1\cdot b_1\cdot b_2 \ldots b_{p-1})_{2}$ having $p$ bits in all, of which $b_0=1$

We will call the set of representable numbers $\mathbb{FP}(p,q;2)$

### Parameters for $\mathbb{FP}(p,q;2)$

The place value of $b_i$ is $2^{-i}$

**Precision**: the number of bits in the significand. Precision = $p$

- The value has 1 representation $(1\cdot0^{p-1})_2\times2^0$
- The smallest positive normalized $\mathbb{FP}$ number greater than 1 has representation $(1\cdot0^{p-1}1)_2\times2^0$ and value $(1+2^{-(p-1)})$

**Machine Epsilon** $\epsilon$: the gap between this number and 1:

$$
\mathcal{E}=2^{-(p-1)}
$$

For an arbitrary normalized FP number $x=\pm S\times 2^E$, the unit in the last place gives the gap between $x$ and the next larger (smaller) normalized FP number, for $x>0$ (for $x<0$), if such a number exists

$$
ulp(x)=\epsilon\times2^E
$$

#### Ex: Toy FP System

Consider a system where all normalized FP numbers have the form $(b_0\cdot b_1b_2)_2\times2^E$, with $E\in \{-1,0,1\}$ and with $b_0 = 1$. What values can this system handle?

| $b_0\cdot b_1b_2$ | $E=-1$ | $E=0$ | $E=1$ | $E=2$ |
| ----------------- | ------ | ----- | ----- | ----- |
| 1.00              | 0.5    | 1     | 2     |       |
| 1.01              | 0.625  | 1.25  | 2.5   |       |
| 1.10              | 0.75   | 1.5   | 3     |       |
| 1.11              | 0.875  | 1.75  | 3.5   |       |
| ulp               | 0.125  | 0.25  | 0.5   |       |

### The Representation of $E$

Suppose we represent $E$ using $q$ bits

- Must handle both positive and negative values of $E$

Define $\text{ebits}_q(E)=W^{-1}_U(E+2^{q-1}-1)$

- We are biasing, why bias?
- We do the bias because it is **much, much easier** to compare a number stored in a biased representation than it is to compare with twos-complement.

When you are encoding, you need to add the bias. Then, once you are trying to decode, subtract the bias.

### Normalized FP Numbers

$$
\text{bias}=2^{q-1}-1
$$

^7ca5db

Minimum representable exponent:

$$
E_{\text{min}}=\text{ebits}_q^{-1}(0^{q-1}1)=1-\text{bias}=-(\text{bias}-1)
$$

^a30730

Minimum normalized **positive** FP number:

$$
N_{\text{min}}=(1.0^{p}1)_2\times2^{E_{\text{min}}}
$$

^e93d90

Maximum representable exponent:

$$
E_\text{max}=\text{ebits}^{-1}_{q}(1^{q-1}0)=\text{bias}
$$

Maximum normalized **positive** FP number:

$$
N_\text{max}=(1.1^{p-1})_2\times2^{E_\text{max}}=(2-2^{-(p-1)})\times2^{E_\text{max}} \approx 2^{E_\text{max}+1}
$$

$2^{-(p-1)}$ is machine epsilon $\mathcal{E}$.

So, in all, we need $p+q$ bits.

### How to interpret the mantissa

The mantissa can be interpreted using a simple property. Reading each bit from the left (ignore endian-ness, and instead look at this from a human reading form), we simply multiple the bit by $2^{-\text{bit number (starting at 1)}}$.

#### Example:

Given the binary representation `0 0001 001` of a floating point (FP(p,q; 4)) number $x$, what is $(x)_{10}$?

We know that there are 4 precision and exponent bits each.

1. See that the sign bit is 0, so this number will be positive
2. The exponent is $1\times2^0-7$ (because the [[Floating Point Numbers#^7ca5db|bias]] is $2^{4-1}-1$) = $-6$
3. The mantissa is $1.0\;\text{(hidden bit)} + 2^{-1} \times 0 + 2^{-2}\times 0 + 2^{-3}\times 1=1.125$.
4. Combining all of these values: $2^{E}\times\text{mantissa}$
   1. $2^{-6}\times1.125=0.017578125$

Note that this was also us finding $N_\text{min}$! The equation for that is [[Floating Point Numbers#^e93d90|here]].

### How to Represent Zero

Since zero is unique, we have a special case

The value 0 has two unique representations:

#### Gaps at Zero

Because we would never be able to approach zero because of the idea of halving, we decide to take equal steps from $N_\text{min}$ to zero.

##### Subnormal Numbers

Extend $\text{ebits}^{-1}_q(E)$ by defining $\text{ebits}^{-1}_q(0^q)=E_\text{min}$, note that this is not equal to $E_\text{min}-1$

Now, if $\text{ebits}^{-1}_q(E)=0^q$, then treat the hidden bit $b_0$ as 0 rather than 1 in calculating the value.

$$
s0^qb_1\ldots b_{p-1}=\pm(0.b_1\ldots b_{p-1})_2
\times2^{E_\text{min}}
$$

Essentially, we interpret the mantissa as we do [[Floating Point Numbers#How to interpret the mantissa|regularly]], except we set the hidden bit to `0`, so it becomes `0.<mantissa>`, and then we multiply by the smallest exponent we can represent, which is given by:
![[Floating Point Numbers#^a30730]]

So, how can we actually interpret a subnormal number?

###### Interpreting Subnormal Numbers

Given the binary representation `0 0000 101` of a floating point (FP(p,q; 4)) number $x$, what is $x$?

We know that there are 4 precision and exponent bits each.

1. See that the sign bit is 0, so this number will be positive
2. The exponent is all zeroes, so it must be a subnormal number (of course it is, that's the point of this problem). Because this is our special case, we arbitrarily set the exponent to [[Floating Point Numbers#^a30730|E min]] ($E_\text{min}$)
   1. $E_\text{min}$ can be found by doing $-((2^{q-1}-1)-1)=-(\text{bias}-1)$
   2. So: we do $-((2^{4-1}-1)-1)=-((8-1)-1)=6$
3. **Because the exponent is all zeroes, the hidden bit also becomes 0**, therefore: The mantissa is $0.0\;\text{(hidden bit) } + 2^{-1} \times 1 + 2^{-2}\times 0 + 2^{-3}\times 1=0.625$.
4. Combining all of these values: $2^{E}\times\text{mantissa}$
   1. $2^{-6}\times0.625=0.0009765625$

### Infinities

Similar to expressing 0, we need to somehow express infinity (but its a concept, not an actual number, so how?)

We point to infinity, but don't actually write it out. How?

We write all `1`'s.

The pattern $01^q0^{p-1}$ will represent the value $+ \infty$

The pattern $11^q0^{p-1}$ will represent the value $-\infty$

### Not a Number (NaN)

What are the results of numbers like $\frac{1}{0}, \frac{1}{\infty}, \infty + \infty$

- These situations are well defined in terms of limits: $\infty, 0, \infty$

But: $0\times\infty, \frac{0}{0},\infty-\infty$; or the square root of a negative number?

- These are "ill-defined" or undefined
- These numbers must become `NaN`'s, and they must **propagate** throughout operations. `1 + NaN = NaN`

Any representation with $\text{ebits}_q(E)=1^q$ but significand $\neq 0^{p-1}$ is a `NaN`.

Multiple `NaN`'s are unordered, but they may be used to represent what kind of illegal operation you hit (e.g., dividing by 0, negative square root, etc.)

### Rounding

Why?

We have defined the finite subset $\mathbb{FP}(p,q)$ of $\mathbb{R}^+=\mathbb{R}\cup\{-\infty,+\infty\}$. How can we reasonably represent an _arbitrary_ extended real number $x\in\mathbb{R}^+$ ignoring `NaN`'s

#### Defining $x$

We define $x$ to be within the normalized range if $N_\text{min}\leq |x|\leq N_\text{max}$

If $x\notin \mathbb{FP}(p,q)$, then one of the following must hold:

1. $x$ is not within the normalized range
2. $x$ is within the normalized range but its representation requires more than $p$ significand bits to represent exactly (imagine $1+2\times10^{-25}$)

#### Sandwiching $x$

We want to sandwich $x$ between two numbers, because that means that we can round it up or down towards a value.

Therefore, we define:

- $x_{-} = \text{max}\{y\in\mathbb{FP}(p,q):y\leq x\}$
- $x_{+} = \text{min}\{y\in\mathbb{FP}(p,q):y\geq x\}$

Basically ceiling and floor functions

With these definitions, we can say that

- $x\in[x_-, x_+]$
- The range $[x_-,x_+]$ is tight
- The range collapses to the single point $x$ iff $x\in\mathbb{FP}(p,q)$

Representing $x_-$ and $x_+$

If $x$ is a positive real number in the normalized range whose exact, possibly infinite representation is

$$
x=(1.b_1\ldots b_{p-1}b_pb_{b+1}\ldots)_2\times2^E
$$

**Then:**

$x_-=(1.b_1\ldots b_{p-1}b_pb_{b+1}\ldots)_2\times2^E$

If $x\notin \mathbb{FP}(p,q)$: $x_+=((1.b_1\ldots b_{p-1})_2+(0.0^{p-2}1)_2)\times2^E$

There is still a corner case where $x_+$ will be re-encoded, but the result will remain a normalized FP number

If $x\notin \mathbb{FP}(p,q)$, then either the lsb of $x_-$ is 0 and the lsb of $x_+$ is 1, or vice versa.

##### Corner Cases

If $x>N_\text{max}$, then define $x_-=N_\text{max}$ and $x_+=+\infty$

If $0<x<N_\text{min}$, then $x_-$ is either a subnormal number, or zero, and $x_+$ is either a subnormal or $N_\text{min}$

Reflect around 0 for negative numbers.

#### Round Function

For $x\in\mathbb{R}^+$, if $x\in\mathbb{FP}(p,q)$, $\text{ROUND}(x) = x$

Otherwise, $\text{ROUND}(x)$ depends on the mode:

- Round down (RD): $\text{ROUND}(x)=x_-$
- Round up (RU): $\text{ROUND}(x)=x_+$
- Round-to-zero (RTZ): $\text{ROUND}(x)=\text{if } x>0 \text{ then } x_- \text{ else } x_+$
- Round-to-nearest, with tiebreak to even (RTE): $\text{ROUND}(x)=$ whichever of $x_-$ or $x_+$ is closer to $x$
  - If there is a tie, choose the one whose significand has lsb = 0

#### Rounding Arithmetic

Note: After **every single** arithmetic operation, a round is performed.

### Floating Point Exceptions and Responses

1. Invalid operation: Set result to NaN
2. Division by zero: Set result to $\pm\infty$
3. Overflow: Set result to $\pm\infty$ or $\pm N_\text{max}$
4. Underflow (subnormal): Set result to $\pm0,\pm N_\text{min}$, or subnormal
5. Inexact (common): Set to correctly rounded value described above.
