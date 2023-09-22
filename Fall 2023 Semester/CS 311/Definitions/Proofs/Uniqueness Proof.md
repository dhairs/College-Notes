## Definition
Recall what uniqueness looks like in terms of quantifiers:
> $$(\exists x|x\in D: P(x)\wedge(\forall y|y\in D: P(y)\to y=x))$$

- Some [[Theorems|theorems]] assert the existence of a *unique* element (aka only one element with a certain property)

**Uniqueness Proofs have two parts**:
1. Existence: We show that such an element $x$ with the desired property exists
2. Uniqueness: We show that if $x$ and $y$ both have the property, then $x=y$ because its unique, so only one possible element.

## Example: Show that if $a$ and $b$ are real numbers $a\neq0$ then there is a unique real number $r$ such that $ar+b=0$

### Proof:
Let's note that the real number $r=\frac{-b}{a}$ is a solution of $ar+b=0$, since $a(\frac{-b}{a})+b=0$

So a real number exists for $ar+b=0$ where $a$ and $b$ are arbitrary real numbers

Second, let's suppose that $s$ is a real number such that $as+b=0$, then its $ar+b=as+b$, where $r=\frac{-b}{a}$

Subtracting $b$ from both sides, and dividing by $a$, since $a\neq0$, we see that $r=s$.