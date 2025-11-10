## Routh Array Stability
- A way to know stability of higher order polynomials
- Necessary (but not sufficient) condition is all coefficients are positive
### Solving the Array
- If $a(s)=1s^n+a_{1}s^{n-1}+a_{2}s^{n-2}+a_{3}s^{n-3}+\dots+a_{n-1}s+a_{n}$
$$
\begin{bmatrix}
1 & a_{2} & a_{4} & a_{6} \\
a_{1} & a_{3} & a_{5} & a_{7} \\
b_{1} & b_{2} & b_{3} & b_{4} \\
c_{1} & c_{2} & c_{3} & c_{4}
\end{bmatrix}
$$
- First row has even coefficients and second row has odd coefficients
- We solve for later rows using the following formula
$$
b_{1}=-\frac{\det \begin{bmatrix}
1 & a_{2} \\
a_{1} & a_{3}
\end{bmatrix}}{a_{1}}=-\frac{1\cdot a_{3}-a_{2}\cdot a_{1}}{a_{1}}
$$
$$
b_{2}=-\frac{\det \begin{bmatrix}
1 & a_{2} \\
a_{4} & a_{5}
\end{bmatrix}}{a_{1}}=-\frac{1\cdot a_{5}-a_{4}\cdot a_{1}}{a_{1}}
$$
$$
c_{1}=-\frac{\det \begin{bmatrix}
a_{1} & a_{3} \\
b_{1} & b_{2}
\end{bmatrix}}{b_{1}}=-\frac{a_{1}\cdot b_{2}-a_{3}\cdot b_{1}}{b_{1}}
$$
- Each determinant uses the same first column but goes to the next two values
- Each row works with the two rows above
- After completion, if first column of Routh array is positive then system is stable
- The number of sign changes in the first column tells you the number of roots in the RHP
### Using Routh's To Make A System Stable
- Plant: $G(s)=\frac{s+1}{s(s-1)(s+6)}=\frac{b(s)}{a(s)}$ Roots: $s=-6,0,1$
#### Unity Gain
$$
T(s)=\frac{G}{1+G}=\frac{b(s)}{a(s)+b(s)}=\frac{s+1}{s(s-1)(s+6)+(s+1)}=\frac{b_{1}(s)}{a_{1}(s)}
$$
$$
a_{1}(s)=s^3+5s^2-5s+1
$$
- New Poles: $-5.88,0.592,0.287$
#### Forward Gain
$$
T(s)=\frac{KG}{1+KG}=\frac{Kb(s)}{a(s)+Kb(s)}=\frac{b_{1}(s)}{a_{1}(s)}
$$
$$
a_{1}(s)=s(s-1)(s+6)+K(s+1)=s^3+5s^2+(K-6)s+K
$$
Routh Array:
$$
\begin{bmatrix}
1 & K-6 & 0 \\
5 & K & 0 \\
b_{1} & 0 & 0 \\
c_{1} & 0 & 0
\end{bmatrix} \rightarrow \begin{bmatrix}
1 & K-6 & 0 \\
5 & K & 0 \\
\frac{4K-30}{5} & 0 & 0 \\
K & 0 & 0
\end{bmatrix}
$$
- $c_{1}$ tells us that $K>0$ but $b_{1}$ tells us that $\frac{4K-30}{5}>0$ so $K>7.5$ for this system to be stable
## Stability and Tracking
- Making $G(s)$ stable using "pole placement" as your controller
- Controller is of the form $Dc(s)=\frac{K(s+z)}{s+p}$ where $(s+z)$ is used for pole cancellation
$$
Dc(s)=\frac{c(s)}{d(s)}, G(s)=\frac{b(s)}{a(s)}, T(s)=\frac{DG}{1+DG}
=\frac{b_{1}(s)}{a_{1}(s)}$$
$$
a_{1}(s)=a(s)d(s)+c(s)b(s)=0
$$
- If we have $G(s)=\frac{1}{(s+1)(s-1)}$
- Since we **cannot** cancel an unstable pole, we have to cancel the stable one ($s=-1$)
$$
z=1
$$
$$a_{1}(s)=(s+1)(s-1)(s+p)+K(s+1)=0$$
$$
a_{1}(s)=(s+1)[(s-1)(s+p)+l]=(s+1)[s^2+(p-1)s+(K-p)]
$$
- Use canonical from of ODE to find values needed to produce a certain complex pole
$$
s^2+(p-1)s+(K-p)=s^2+2\zeta\omega_{n}s+\omega_{n}^2=s^2+2\sigma s+\omega_{n}^2
$$
- We use this form to find the right $p$ and $K$ that will produce the poles we want
#### Example ($s=-1\pm j2$)
- To set the poles to $s=-1\pm j2$ we know that $\sigma=1$ and $\omega_{d}=2$
$$
\omega_{n}^2=\sigma^2+\omega_{d}^2=1^2+2^2=5
$$
- So $\omega_{n}=\sqrt{ 5 }$
- Now we can solve for $p$ and $K$
$$
p-1=2\sigma
$$
$$
p-1=2
$$
$$
p=3
$$
$$
K-p=\omega_{n}^2
$$
$$
K-3=5
$$
$$
K=8
$$
$$
Dc(s)=\frac{8(s+1)}{s+3}
$$
- This controller will place the closed loop poles at $s=-1\pm j2$
## Steady-state Errors to Polynomial Inputs
- The input $R(s)=\frac{1}{s^{k+1}}$ where $k$ is the *degree* of the input
- The system $GD_{CL}(s)=\frac{GD_{CLO}(s)}{s^n}$ where $n$ is the number of integrators (poles at 0)
- $e_{ss}$ refers to the steady-state error of the system

| $e_{ss}$           | $k=0$ (Step/Position) | $K=1$(Ramp/Velocity) | $K=2$(Parabolic/Acceleration) |
| ------------------ | --------------------- | -------------------- | ----------------------------- |
| $n=0$ **(Type 0)** | $\frac{1}{1+k_{p}}$   | $\infty$             | $\infty$                      |
| $n=1$ **(Type 1**  | $0$                   | $\frac{1}{k_{v}}$    | $\infty$                      |
| $n=2$ **(Type 2)** | $0$                   | $0$                  | $\frac{1}{k_{a}}$             |
- $k_{p}=\lim_{ s \to 0 }GD_{CL}(s)$
- $k_{v}=\lim_{ s \to 0 }s\cdot GD_{CL}(s)$
- $k_{a}=\lim_{ s \to 0 }s^2\cdot GD_{CL}(s)$
### Interpreting the Table
- A system of a certain type can only track the error of input that has a degree that is equal or less
	- if $n>k$, then $e_{ss}=0$
	- If $n<k$, then $e_{ss}\rightarrow\infty$
	- If $n=k=0$, then $e_{ss}=\frac{1}{1+k_{n}}$
	- If $n=k\neq0$, then $e_{ss} = \frac{1}{k_{n}}$
## Root Locus
- A way to determine how the poles move as $K$ varies between $0<K<\infty$
- Follows a set of rules to draw out the loci
- $n=\text{Number of Poles}$
- $m=\text{Number of Zeros}$
### Rule 1
**The $n$ branches of the locus start at the poles of $L(s)$ and $m$ of those branches end on zeroes of $L(s)$**
### Rule 2
**Any portion of the real axis to the left of an odd number of poles and zeros is on the locus**
#### Examples of Rules 1-2 Together
##### $L(s)=\frac{s}{s+4}$
The loci goes from the $-4$ pole to the $0$ pole
- Goes from the pole to the zero according to rule 1
- Is on the real axis because it is to the left of an odd number of poles and zeroes ($1$)
##### $L(s)=\frac{s+4}{s}$
The loci goes from the $0$ pole to the $-4$ zero
- Goes from the pole to the zero according to rule 1
- Is on the real axis because it is to the left of an odd number of poles and zeroes ($1$)
##### $L(s)=\frac{1}{s}$
The loci goes from the $0$ pole to $-\infty$
- Goes from the pole to $-\infty$ according to rule 1
- Is on the real axis because it is to the left of an odd number of poles and zeroes ($1$)
##### $L(s)=\frac{1}{s^3}$
The loci goes from the $0$ pole to $-\infty$
- Goes from the pole to $-\infty$ according to rule 1
- Is on the real axis because it is to the left of an odd number of poles and zeroes ($3$)
- The remaining two loci will be determined using rule 3
### Rule 3
**For large values of $s$ and $K$, the remaining $n-m$ branches of the locus are asymptotic to the lines at angles $\phi_{l}$ radiating out from the point $s=\alpha$ on the real axis**
- $\phi_{l}=\frac{180^{\circ}+360(l-1)}{n-m}$ where $l=1,2,\dots ,(n-m)$
- $\alpha=\frac{\sum p_{i}-\sum z_{i}/}{n-m}$

### Rule 4
**The angles of departure of departure of a locus branch from a pole is given by $\phi_{l}$ and the angles of arrival of a locus branch to a zero is given by $\psi_{l}$**
- $\phi_{l}=\sum \psi_{i}-\sum \phi_{i}-180^{\circ}-360^{\circ}(l-1)$ where $l=1,2,\dots,n$
	- $\sum \psi_{i}$ is the sum of the angles to all the zeros
	- $\sum \phi_{i}$ is the sum of the angles to the remaining poles
- $\psi_{l}=\sum \phi_{i}-\sum \psi_{i}+180^{\circ}+360^{\circ}(l-1)$
	- $\sum \phi_{i}$ is the sum of the angles to all the poles
	- $\sum \psi_{i}$ is the sum of the angles to all the remaining zeros
### Rule 5
**The locus can have multiple roots at points on the locus and the branches will approach a point of $q$ roots at angles separated by $\frac{180^{\circ}+360(l-1)}{q}$ and will depart at angles with the same separation**
### Breakaway and Rejoining Points
- Breakaway points and rejoining points are where the locus break from the real axis and rejoin with it at a later point
- These points occur when $\frac{d}{ds}K(s)=0$
- In root locus form, $1+KL(s)=0$ so $K=-\frac{1}{L(s)}$
- Usually use quotient rule to solve the derivative
$$\frac{d}{dx}\left[ \frac{f(x)}{g(x)} \right]=\frac{g(x)f'(x)-f(x)g'(x)}{(g(x))^2}$$
- Solve for when $g(x)f'(x)-f(x)g'(x)=0$, the roots are the breakaway/rejoining points