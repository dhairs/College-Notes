
- Many theorems are assertions that some object or element of some property/type is true
- These theorems have the form $$(\exists x|x\in D: P(x)).$$
- Proof of this type of theorem is called an **existence proof**
- There are **two** ways theorems are written for this type:
	- Constructive: Find an element $a$, where $a\in D$ for which $P(a)$ is true. $a$ is called a **witness**
	- Nonconstructive: Do not look for a witness, but show that $(\exists x|x\in D: P(x))$ is true another way

### Example 1 (Constructive): Show that there exists a positive number that can be written as a sum of cubes of positive integers in two different ways
$Sol^n: 1729=10^3+9^3=12^3+1^3$

### Example 2 (Non-Constructive): Show that there exists irrational numbers $x$ and $y$ such that $x^y$ is rational

#### Proof
From a previous theorem, we know that $\sqrt2$ is irrational.

Consider the number $\sqrt{2}^\sqrt2$. 

If $\sqrt{2}^\sqrt2$ is rational, then we have two irrational numbers, $x$ and $y$ with $x^y$ being rational.

**BUT. Let's consider the case where we don't know allat**

If $\sqrt{2}^\sqrt{2}$ is irrational, then let $x=\sqrt{2}^\sqrt{2}$ and $y=\sqrt2$.

Now, $$x^y=(\sqrt{2}^\sqrt{2})^\sqrt{2} = \sqrt{2}^2=2$$
Therefore, there exists irrational numbers $x$ and $y$ such that $x^y$ is rational.

Basically, do a bunch of algebraic manipulation to find values that lead to the wanted conclusion.
