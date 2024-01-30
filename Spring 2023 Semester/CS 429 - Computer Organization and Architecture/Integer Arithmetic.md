# Integer Arithmetic

We want to perform the standard collection of integer arithmetic operations: **addition** $(x+y)$, **unary negation/additive inverse** $(-x)$, **subtraction** $(x-y)$, **multiplication** $(x * y)$, **division** $(x/y)$.
- Everything can be defined from addition and additive inverse 

We can't do mathematical addition with $n$-bit representations
- We defined the operations $x\bigoplus y$, $x\bigodot y$  


## Unsigned Integer Addition: $x \bigoplus^{n}_{u} y$ 

Operationally:
- Starting at position $x$ on the unsigned $n$-wheel, move $y$ positions clockwise, ending at the sum

Definition:
- $r=x \bigoplus^{n}_{u} y {\text{def}\atop =}(x+y)\,\text{mod}\,2^n$ 

If we go past the red flag in doing this, we have an **unsigned carry**.

### Properties of Integer Addition $\bigoplus^{n}_{u}$

$\bigoplus^{n}_{u}$ is **commutative** and **associative**

The element $0$ is the unique **identity** for $\bigoplus^{n}_{u}$
- i.e., $\forall x\in U_n: x\bigoplus^{n}_{u}0=x$.

Every element $x$ has a unique **additive inverse** $\ominus^{n}_{u}$
- i.e., $\forall x\in U_n: x\bigoplus^{n}_{u}(\ominus^{n}_{u}x)=0$ 

## Unsigned Integer Subtraction: $x \ominus^{n}_{u}y$ 

Operationally:
- Starting at position $x$ on the unsigned $n$-wheel, move $\ominus^{n}_{u}y$ positions *clockwise* (equivalent to moving $y$ positions counter-clockwise), ending at the difference

Definition:
- $r=x\ominus^{n}_{u}y {\text{def}\atop =} x\bigoplus^{n}_{u}(\ominus^{n}_{u}y)$ 

If we go past the red flag in doing this, we have an **unsigned carry**.

Same properties as integer addition.

## Signed Integer Addition: $x\bigoplus^{n}_{s}y$

Operationally:
- Starting at position $x$ on the signed $n$-wheel, move $y$ positions *clockwise*, ending at the sum. 
	- What if $y<0$?

Definition:
- Let $s=x+y$, this is the mathematical sum
- Then $r=x\bigoplus^{n}_{s}y=

### Signed Overflow: $\bigoplus^{n}_{s}$

If we go past the red flag in *either direction* while doing this, we have a **signed overflow**

Detection is **value based**

### Properties of $\bigoplus^{n}_{s}$

$\bigoplus^{n}_{s}$ is **commutative** and **associative**

The element $0$ is the unique **identity** for $\bigoplus^{n}_{s}$
- i.e., $\forall x\in S_n: x\bigoplus^{n}_{u}0=x$

Every element $x$ has a unique **additive inverse** $\ominus^{n}_{u}x$ 
- i.e., $\forall x\in S_n: x\bigoplus^{n}_{u}(\ominus^{n}_{u}x)=0$


### Example Additive Inverse $\ominus^3_sx$ 

| Repr$x$ | $x$ | $\ominus^3_sx$ | Repr($\ominus^3_sx$) | ~Repr($x$) | ~Repr($x$)+1 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 000 | 0 | 0 | 000 | 111 | 000 |
| 001 | 1 | -1 | 111 | 110 | 111 |
| 010 | 2 | -2 | 110 | 101 | 110 |
| 011 | 3 | -3 | 101 | 100 | 101 |
| 100 | -4 | -4 | 100 | 011 | 100 |
|  |  |  |  |  |  |


### Multiplication: $\bigodot^n_u$ and $\bigodot^n_s$

Operationally (not very useful):
- Iterated addition — literally definitionally what multiplication is
- Adjust appropriately for signed

Definition:
- **Unsigned**: $x\bigodot^n_uy\;{\text{def} \atop =}\;(x\cdot y)\,\text{mod}\,2^n$ 
- **Signed**: $x\bigodot^n_sy\;{\text{def} \atop =}\;U2S_n((x\cdot y)\,\text{mod}\,2^n)$ 

$U2S$ means Unsigned to Signed
$S2U$ means Signed to Unsigned