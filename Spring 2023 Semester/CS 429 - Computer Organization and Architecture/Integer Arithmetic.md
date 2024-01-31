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
- Then $r=x\bigoplus^{n}_{s}y=$ 

### Signed Overflow: $\bigoplus^{n}_{s}$

If we go past the red flag in *either direction* while doing this, we have a **signed overflow**

Detection is **value based**

### Properties of $\bigoplus^{n}_{s}$

$\bigoplus^{n}_{s}$ is **commutative** and **associative**

The element $0$ is the unique **identity** for $\bigoplus^{n}_{s}$
- i.e., $\forall x\in S_n: x\bigoplus^{n}_{u}0=x$

Every element $x$ has a unique **additive inverse** $\ominus^{n}_{u}x$ 
- i.e., $\forall x\in S_n: x\bigoplus^{n}_{u}(\ominus^{n}_{u}x)=0$


## Example Additive Inverse $\ominus^3_sx$ 

| Repr$x$ | $x$ | $\ominus^3_sx$ | Repr($\ominus^3_sx$) | ~Repr($x$) | ~Repr($x$)+1 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 000 | 0 | 0 | 000 | 111 | 000 |
| 001 | 1 | -1 | 111 | 110 | 111 |
| 010 | 2 | -2 | 110 | 101 | 110 |
| 011 | 3 | -3 | 101 | 100 | 101 |
| 100 | -4 | -4 | 100 | 011 | 100 |
|  |  |  |  |  |  |

## Multiplication: $\bigodot^n_u$ and $\bigodot^n_s$

Operationally (not very useful):
- Iterated addition — literally definitionally what multiplication is
- Adjust appropriately for signed

Definition:
- **Unsigned**: $x\bigodot^n_uy\;{\text{def} \atop =}\;(x\cdot y)\,\text{mod}\,2^n$ 
- **Signed**: $x\bigodot^n_sy\;{\text{def} \atop =}\;U2S_n((x\cdot y)\,\text{mod}\,2^n)$ 
	- First calculate the unsigned value, then convert to a signed value.

$U2S_n$ means Unsigned to Signed - We need this one because of the definition of the mod operator.

$S2U$ means Signed to Unsigned

### Ex: $x\bigodot^3_uy$ with $x=5$ and $y=6$

$$
\begin{align}
2^n=2^3=8\\
5\times6 = 30 = 3\times8+6
\end{align}
$$

### Ex: $x\bigodot^3_uy$ with $x=3$ and $y=-2$

$$
\begin{align}
2^n=2^3=8 \\
3\times-2=-6=-1\times8+2
\end{align}
$$

### Ex: $x\bigodot^3_uy$ with $x=3$ and $y=-3$

$$
\begin{align}
2^n=2^3=8 \\
3\times-3=-9=-2\times8+7
\end{align}
$$

The number's $-2$ and $7$ are chosen because we have defined $\text{mod}$ to not be negative. So we must go farther and then step back.

In this case, we go to $-16$ and then move upwards back to $-9$.


### Multiplication by Constants

For $0\leq k < n$:
- $x\bigodot^n_u2^k=x<<k$
- $x\bigodot^n_s2^k=x<<k$

This gives us a way of simplifying multiplying by constants using shifts and adds (**strength reduction**).

**Ex:** $x\times 14 = x\times 8 + x\times 4 + x\times 2 = (x<<3) + (x<<2) + (x<<1)$. 

## Floor and Ceiling Functions

For any real number $x$, we define:
- floor($x$), written $\lfloor x\rfloor$, to be the greatest integer less than or equal to $x$
- ceil($x$), written $\lceil x\rceil$, to be the smallest integer greater than or equal to $x$

If $n$ is an integer, then $\lfloor n\rfloor = \lceil n\rceil = n$ 

Otherwise, $\lfloor n\rfloor = \lceil n\rceil - 1$

## Integer Division by Constants

For $0\leq k < n$:
- **Unsigned**: $x >>_L k$ yields $\lfloor x/2^k \rfloor$ 
- **Signed**: $x>>_A k$ yields $\lfloor x/2^k \rfloor$ 
- **Signed**: $(x+(1<<k)-1)>>_A k$ yields $\lceil x/2^k \rceil$
	- We first bias the value and *then* perform the shift
	- $1<<k=1\times 2^k=2^k-1$  

## Implementing Addition

**Very, *very*** similar to a grade school addition algorithm.

| **s** | **0** | **1** |
| ---- | ---- | ---- |
| **0** | 0 | 1 |
| **1** | 1 | 0 |

| **+** | **0** | **1** |
| ---- | ---- | ---- |
| **0** | 00 | 01 |
| **1** | 01 | 10 |

| **C** | **0** | **1** |
| ---- | ---- | ---- |
| **0** | 0 | 0 |
| **1** | 0 | 1 |

### $n$-bit Adder

We want $(s[n-1:0],c)=SUM(a[n-1:0],b[n-1:0])$


Literally think of regular addition but in base 2, so instead of reaching 10 and then carrying, we carry when we reach 2.

We use the **ripple-carry adder** scheme
- $(s[0], c_{out}[0])=FA(a[0],b[0],0)$
- $\forall i \in [1:n-1], (s[i], c_{out}[i])=FA(a[i],b[i], c_{out}[i-1])$ 
- $c=c_{out}[n-1]$


### $n$-bit Subtractor

We want $(d[n-1:0],c)=DIFF(a[n-1:0],b[n-1:0])$

We will implement this by using the definition of subtraction in terms of addition and additive inverse:

$$
a-b=a+(-b)=a+\overline{b}+1
$$

Literally think of regular addition but in base 2, so instead of reaching 10 and then carrying, we carry when we reach 2.

We still use the **ripple-carry adder** scheme
- $(d[0], c_{out}[0])=FA(a[0],b[0],1)$
- $\forall i \in [1:n-1], (d[i], c_{out}[i])=FA(a[i],b[i], c_{out}[i-1])$ 
- $c=c_{out}[n-1]$

