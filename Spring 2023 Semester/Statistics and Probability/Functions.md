## Functions of Random Variables

Functions of random variables are also random variables.

If $Y=g(x)$ then we have:

$$
p_y(y)=\sum_{\{x|g(x)=y\}}p_x(x)
$$

## Cumulative Distribution Function (CDF)

The cumulative distribution function (CDF) of a random variable is the function:

$$
F(x)=P(X\leq x)
$$

The CDF gives us the probability that the variable takes a value less than or equal to $x$. 

A property of CDF's: $0\leq F(X)\leq 1$ for all $x$.

### Example: Obtaining the CDF from the PMF

Suppose the range of a discrete random variable is $\{0,1,2,3,4\}$ and its probability mass function is $P(X=x)=\frac{x}{10}$

For $x<1$, $F(x)=\sum_