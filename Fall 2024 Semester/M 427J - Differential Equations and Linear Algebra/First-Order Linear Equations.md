## Definition

A first order linear equation is of the form:

$$
\frac{dy}{dt}+a(t)y=b(t)
$$

Where $a$ and $b$ are continuous functions.

### Homogeneous First Order Linear Equation
If $b(t)=0$, we will say that the equation is homogeneous.

$$
\frac{dy}{dt}+a(t)y=0
$$

### Initial Condition

Sometimes, there will be an extra equation that we will call the initial condition. Typically of the form:

$$
y(t_{0})=y_{0}
$$

Where $y(t)$ is the solution function. The subscript $\text{var}_0$ just signifies the initial condition or state.

## Solving First-Order Linear Equations

Given $a(t)$, we define a new function called the **integrating factor**. We have:

$$\mu(t)=\exp\left[ \int a(t)dt \right]$$

Where $\int a(t)dE$ is any antiderivative of $a(t)$

**Remark**: The exponential function is $\exp(Z)=e^Z$, thus $\mu(t)=\exp\left[ \int a(t)dt \right]=e^{\int a(t)dt}$

**Remark**: If we have an initial condition $y(t_{0})=y_{0}$, it is convenient to use

$$\int a(t)dt=\int_{t_{0}}^t
a(s)ds$$
***
If $u=\int a(t)dt$ then $\mu(t)=e^u$ and $\frac{d\mu}{dt}=\frac{d}{dt}e^u=e^u \frac{du}{dt}$

We conclude $$
\frac{du}{dt=\mu(t_{1}a(t))}
$$
If $y(t)$ satisifies


$$
\frac{d}{dt}(\mu(t)y(t))=\frac{d\mu}{dt}y(t)+\mu(t) \frac{dy}{dt}
$$

After substitution, we find

$$
\begin{align}
\frac{d}{dt}(\mu(t)y(t))=\mu(t)a(t)y(t)+\mu(t)[-a(t)y(t)+b(t)] \\ \\
= 
\end{align}
$$

### Useful Antiderivatives

$$
\begin{align}
\int e^{at}\cos(bt)dt=\frac{e^{at}}{a^2+b^2}(a\cos(bt)+b(\sin(bt))) \\
 \\
\int e^{at}\sin(bt)dt=\frac{e^{at}}{a^2+b^2}(a\sin(bt)-b(\cos(bt))) \\
 \\
\text{where a and b are constants}
\end{align}
$$

#### Example

Find the general solution of

$$
\frac{dy}{dt}+2y=10\sin(t)
$$

There is no initial value, so the solution will include a constant.

We use $a(t) =2$ and $b(t)=10\sin(t)$.

The integrating factor is

$$
\mu(t)=\exp\left[ \int a(t)dt \right]=\exp[2t]
$$

$$
\frac{d}{dt}(e^{2t}y(t))=10e^{2t}\sin(t)
$$

This implies that

$$
\begin{align}
e^{2t}y(t)=\int 10e^{2t}\sin(t)dt \\
=10\int e^{2t}\sin(t)dt \\
=10 \frac{e^{2t}}{4+1}(2\sin(t)-\cos(t)) \\ \\

=2e^{2t}(2\sin(t)-\cos(t)) \\ \\

4e^{2t}\sin(t)-2e^{2t}
\cos(t) + C \\
\end{align}
$$


### Example with DE given in correct form

Solve

$$
\frac{dy}{dt} + 2y=5e^{3t} \text{ with } y(0)=-10
$$

In this case, $a(t)=2$, $b(t)=5e^{3t}$.

We have an initial condition $y(t_{0})_=y_{0}$ where $t_0=0$ and $y_0=-10$.

The integrating factor is:

$$
\begin{align}
\mu(t)=\exp\left[ \int a(t)dt \right]=\exp\left[ \int_{2}dt \right] \\
= \exp[2t]=e^{2t}
\end{align}
$$

We use the formula

$$
\frac{d}{dt}(\mu(t)y(t))=\mu(t)b(t)
$$

In our case,

$$
\frac{d}{dt}(e^{2t}y(t))=e^{2t}5e^{3t}=5e^{5t}
$$

Find antiderivatives:

$$
e^{2t}y(t)=\int 5e^{5t}dt=e^{5t}+C
$$

We have that $e^{2t}y(t)=e^{5t}+C$. We need to find $C$, so we can use the initial condition from earlier $y(0)=-10$. Substitute $t=0$ into the equation we have.

Thus:

$$
\begin{align}
y(0)=1+C=-10 \\
C=-11
\end{align}
$$

We can now substitute $C$ into the equation, and get $e^{2t}y(t)=e^{5t}-11$. Solving for $y(t)$, we divide by $e^{2t}$ and get:

$$
y(t)=e^{3t}-11e^{-2t}
$$

This is the solution to the differential equation. 

We can verify the solution by computing the left-hand side (LHS) and compare with the right-hand side (RHS) of the equation.

We have: 
$$
\begin{align}
\frac{dy}{dt}+2y=3e^{3t}+22e^{-2t}+2(e^{3t}-11e^{-2t}) \\
=3e^{3t}+2e^{3t}=5e^{3t}
\end{align}
$$

In addition, $y(0)=1-11(1)=-10$ which satisfies the initial condition.


### Example with DE given in incorrect form

Solve

$$
t \frac{dy}{dt}-3y=10t^7 \text{ with } y(1)=6 
$$

This is not in the form of our expected pattern, so we need to divide by $t$ to get that.

$$
\frac{dy}{dt}-\frac{3y}{t}=10t^6
$$

In this case, $a(t)=-\frac{3}{t}$, $b(t)=10t^6$

The integrating factor is $\mu(t)=\exp\left[ \int a(t)dt \right]=\exp\left[ -3 \int \frac{1}{t}dt \right]$

We have the formula:

$$
\frac{d}{dt}(\mu(t)y(t))=\mu(t)b(t)
$$

In this case, $\frac{d}{dt}(t^{-3}y(t))=t^{-3}10t^6=10t^3$. Now we can find the antiderivatives:

$$
\begin{align}
t^{-3}y(t)=\int 10t^3dt=\frac{5}{2}t^4+C
\end{align}
$$

Now find the constant $C$ using the initial condition $y(1)=6$:

$$
\begin{align}
y(1)=\frac{5}{2}+C=6 \\
C=6-\frac{5}{2}=\frac{7}{2}
\end{align}
$$

Substitute this value back into the solution, and we get:

$$
\begin{align}
t^{-3}y(t)=\frac{5}{2}t^4+\frac{7}{2}
\end{align}
$$

Solving for $y(t)$,

$$
y(t)=\frac{5}{2}t^7
+\frac{7}{2}t^3
$$

