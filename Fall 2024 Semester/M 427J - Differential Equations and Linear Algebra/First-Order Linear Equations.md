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