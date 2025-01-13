
## Definition

Consider a [[Semesters/Fall 2024 Semester/M 427J - Differential Equations and Linear Algebra/Introduction to Differential Equations|differential equation]] of the form 

$$\frac{dy}{dt}=\frac{g(t)}{f(y)}$$

Such an equation is called separable because we can separate the variables.

If $y(t)$ satisfies the equation, then

$$
y'(t)=\frac{dy}{dt}=\frac{g(t)}{f(y(t))}
$$

Let $F(y)$ be an antiderivative of $f(y)$. Using the chain rule,

$$
\begin{align}
\frac{d}{dt}F(y(t))=F'(y(t))*y'(t) \\
=f(y(t)) \frac{g(t)}{f(y(t))}=g(t)
\end{align}
$$

So, $F(y(t))$ is an antiderivative of $g(t)$.

### Formula

We get the following formula:

$$
\int f(y)dy=\int g(t)dt+C
$$