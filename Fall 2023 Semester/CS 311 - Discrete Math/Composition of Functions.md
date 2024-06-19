# Definition
Remember that functions map [[Sets.md|sets]]
$g: A\to B$

$f: B\to C$

The composition of functions $f\circ g: A\to C$

$$f\circ g(a) = f(g(a))$$

Domain of $f\circ g$ = Domain of $g$

Codomain of $f\circ g$ = Codomain of $f$

Codomain of $g\subseteq$ domain of $f$

Range of $f\circ g=$ The image of range of $g$ under the function $f$

Range of $g=S$ (subset of codomain of $g$)

[[Matrix Multiplication.md]] can also be understood as a composition of functions.


Function
$$
\text{Codomain of F is} \;\;
\begin{align}
\mathbb{R} \;\text{(real-valued)} \\
\mathbb{Z} \;\text{(integer-valued)}
\end{align}
$$



# Example
$$\begin{align}
A=\{a,b,c\} \\
C=\{1,2,3\} \\ \\
g: A\to A \\
g(a) = b && g(b) = c && g(c) = a \\ \\
f: A\to C \\
f(a) = 3 && f(b) = 2 && f(c) = 1 \\ \\
f\circ g: A\to C \\
f\circ g(a) = f(g(a)) \\
= f(b) \\
= 2 \\ \\
f\circ g(b) = f(g(b)) \\
= f(c) \\
= 1 \\ \\
f(g(c)) = f(a) \\
= 3 \\
\end{align}
\text{NOTE:}\; g\circ f \; \text{NOT DEFINED BECAUSE g IS A SUBSET OF f}$$


