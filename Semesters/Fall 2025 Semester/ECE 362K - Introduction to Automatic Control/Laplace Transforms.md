
## Laplace Transform

Extremely useful for solving differential equations, but also helps transforms functions/waveforms **from** the **time** domain **to** the **frequency** domain.

The notation for Laplace transforms is:

$$
\cal L\{f(t)\} \to F(s)
$$

### What is a Transform?

Sort of a function of functions. Similar to how some functions take us from one set of numbers to another set. **Transforms** take us from one set of functions to another set of functions. 

### Definition of Laplace Transform

$$
\cal L\{f(t)\}=\int_{0}^\infty e^{-st}f(t)dt
$$

This is an [[Improper Integrals|improper integral]].

### Laplace Transform Table

These are well known Laplace transforms. Some of the derivations are shown below.

$$
\cal L\{1\}=\frac{1}{s}
$$

### Derivation of Laplace Transform on 1

$$
\begin{align}
\cal L\{1\}=\int_{0}^\infty e^{-st}dt  = \lim_{ A \to \infty } \int_{0}^Ae^{-st}dt \\
= \lim_{ A \to \infty } \left[  -\frac{1}{s}e^{-st} \right]^A_{0} =\lim_{ A \to \infty } \left( -\frac{1}{s}e^{-sA}-\left( -\frac{1}{s} \right) \right)  \\
\lim_{ A \to \infty } \left[ -\frac{1}{s}e^{-sA}+\frac{1}{s} \right] \text{for } s>0 =\frac{1}{s}
\end{align}
$$

### Derivation of Laplace Transform on $e^{at}$

$$
\begin{align}
\cal L\{e^{at}\}=\int_{0}^\infty e^{-st} e^{at}dt=\int_{0}^\infty e^{(a-s)t}dt \\
=\frac{1}{a-s}[e^{(a-s)t}]^\infty_{0}=\frac{1}{a-s}[]
\end{align}
$$

## System Response

Imagine we have $x(t)\to H\to y(t)$. Where $H$ is some black box that performs a function on input signal $x(t)$. We want to find output signal $y(t)$.

The **system** $H$ can be described as:
- Differential Equation (ODE) $a_{2}y''(t)+a_{1}y'(t)+a_{0}y(t)=b_{0}x(t)$
- Difference Equation $a_{0}y[n]+a_{1}y[n-1]+a_{2}y[n-2]=\beta_{0}x[n]$
- Impulse Response $h(t)$
- Step Response $h_{1}(t)$
- Frequency Response $H(jw)$
- Transfer Function $H(S)$
- Block Diagrams

## Input Signals

The input signal $x(t)$ was generally limited to either
- Impulse $x(t)=S(t)$
- Step $x(t)=u(t)$
- Ramp $x(t)=t(wt)$

## Transforms

Time domain:

$$
1. \text{Convolution: } \; y(t)=x(t)\times h(t)=\int_{-\infty}^\infty x(\tau)h(t-\tau)dt
$$

By transforming the time domain problem into the frequency domain, we changed from **convolution to multiplication**. That means that the ODE is solved by algebraic techniques.

Eventually, we get to to $Y(s)$, but we want to get $Y(t)$.

We look to the [[Inverse Laplace Transform]].

