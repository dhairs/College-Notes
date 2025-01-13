## Type 1 Improper Integral: $\infty$ in the bounds

### When the Improper Integral has $\infty$ in one of the bounds

Let $f$ be a function and let $a$ be a real number.

(Type 1) We define $\int_{a}^{\infty}f(x)\mathrm{d}x \to \lim_{t\to\infty}\int_{a}^{t}f(x)$

##### When the limit exists: "The improper integral is convergent"

> The value of a convergent improper integral is the **value of the limit.**

##### When the limit D.N.E: "The improper integral is divergent"

#### Rewriting Improper Integrals with a $\infty$ in a single bound

Get rid of the infinity in the bounds and add a limit with bound $t$ (or any other unused variable).
$\int_{0}^{\infty} f(x) \to \lim_{t\to\infty}\int_{0}^{t}f(x)$

### When the improper integral is from $-\infty$ to $\infty$

(Type 1) We define $\int_{-\infty}^{\infty}f(x)\mathrm{d}x$

Split up the integral to define it. let $a$ be any real number.

If $\int_{a}^{\infty}f(x)\mathrm{d}x$ is convergent
**AND**
If $\int_{-\infty}^{a}f(x)\mathrm{d}x$ is convergent

Then $\int_{-\infty}^{\infty}f(x)\mathrm{d}x$ is convergent:
$\int_{-\infty}^{\infty}f(x)\mathrm{d}x = \int_{-\infty}^{a}f(x)\mathrm{d}x + \int_{a}^{\infty}f(x)\mathrm{d}x$

If **either of the split up integrals are divergent, the whole term is divergent as well.**

## Type 2 Improper Integral: discontinuous function

When the function is not continuous at:
$a$: $\int_{a}^{b}f(x)\mathrm{d}x \to \lim_{t\to a^{+}}\int_{t}^{b}f(x)\mathrm{d}x$
$b$: $\int_{a}^{b}f(x)\mathrm{d}x \to \lim_{t\to b^{-}}\int_{a}^{t}f(x)\mathrm{d}x$
