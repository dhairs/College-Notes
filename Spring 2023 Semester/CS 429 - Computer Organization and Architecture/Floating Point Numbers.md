## The Design Problem

With 64-bit integers, we only get `18,446,744,073,709,600,000` distinct values. But quantities in physics and mathematics can easily go well beyond this.

We need to find something that is not only efficient in storage space, but also in computational time, because we only have so many resources.

![[Floating Point Design Problem.excalidraw]]

## Choice 1: Fixed Point

Represent a number $x$ as $\pm x_i * x_f$ where:
- $x_i$ is the integer part of $x$, represented using $a$ radix-$k$ digits
- - $x_f$ is the fractional part of $x$, represented using $b$ radix-$k$ digits

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
- Not an infinite number of bits after binary point, so $S=(1\cdot b_1\cdot b_2 \ldots b_{p-1})_{2}$  having $p$ bits in all, of which $b_0=1$ 

We will call the set of representable numbers $\mathbb{FP}(p,q;2)$


## Parameters for $\mathbb{FP}(p,q;2)$

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
### Ex: Toy FP System

Consider a system where all normalized FP numbers have the form $(b_0\cdot b_1b_2)_2\times2^E$, with $E\in \{-1,0,1\}$ and with $b_0 = 1$. What values can this system handle?

| $b_0\cdot b_1b_2$ | $E=-1$ | $E=0$ | $E=1$ | $E=2$ |
| ---- | ---- | ---- | ---- | ---- |
| 1.00 | 0.5 | 1 | 2 |  |
| 1.01 | 0.625 | 1.25 | 2.5 |  |
| 1.10 | 0.75 | 1.5 | 3 |  |
| 1.11 | 0.875 | 1.75 | 3.5 |  |
| ulp | 0.125 | 0.25 | 0.5 |  |

## The Representation of $E$

Suppose we represent $E$ using $q$ bits