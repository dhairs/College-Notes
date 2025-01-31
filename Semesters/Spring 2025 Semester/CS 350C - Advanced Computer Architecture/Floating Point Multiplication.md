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

## Floating Point Multiplier Design

Input:
- Two [[Floating Point Numbers#Normalized FP Numbers|normalized]] floating point number $x$ and $y$

Outputs:
- $p=\text{ROUND}(x\cdot y)$
- $\text{Err}=\text{Error Flag}$

![[FP Multiplier.svg]]

### Shift and Add Multiplier

When the state machine is at state ST'/0, all outputs are 0, and the machine is waiting for start signal.

