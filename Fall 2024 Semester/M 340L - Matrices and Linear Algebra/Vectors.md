## Definition

A vector is a list of *real* numbers.

### Example

$$

\bar{v}=\begin{bmatrix}
1 \\
2 \\
3
\end{bmatrix}, (1,2,3)
$$

Elements are 1-indexed, and for column (vertical) vectors, the topmost value is 1st, for row (horizontal) vectors, the leftmost value is 1st.

In this class, $\bar{}$  is the notation for a vector.

## Notation

$\text{R}^2$ is the set of all vectors of size 2.
***
$\text{R}^n$ is the set of all vectors of size $n$.

### Example

$$
\bar{0}=\begin{bmatrix}
0 \\
0 \\
\vdots \\
0
\end{bmatrix}
$$

This is a zero vector, all entries in it are zeroes.

## Interpretations of Vectors

- List of numbers
- Point
	- Ex. a vector of size 2 can be interpreted as coordinate points in a 2-dimensional plane.
	- $n$ size vectors can be used to represent $n$-dimensional space/planes.
- Arrow (*note that different arrows may represent the same vector*)
- Displacements

![[Vector.svg]]

To obtain a vector from point $P$ to $Q$, subtract the coordinates of $P$ from $Q$ (this will give you the distance between each component of the coordinates). $\bar{v}=Q-P$.

## Operations with Vectors

### Addition

If $\bar{v}$ and $\bar{w}$ are vectors of size $n$, then you can add every corresponding values in vectors:

$$
\bar{v}+\bar{w}=
\begin{bmatrix}
v_{1}+w_{1} \\
v_{2}+w_{2} \\
\vdots \\
v_{n}+w_{n}
\end{bmatrix}
$$

Note that you *cannot* add vectors of different sizes.

#### Adding Vectors as Arrows

To add two arrows as vectors, move the start of one arrow to the end of the other, and then connect the start of the first arrow to the end of the second arrow. (Essentially add the components of the vectors as you would normally)

![[Adding Vectors as Arrows.svg]]

Note that this creates a parallelogram.

#### Example of Adding Two $n$-size Vectors

$$
\begin{bmatrix}
1 \\
2  \\
3
\end{bmatrix}
+
\begin{bmatrix}
-1 \\
0 \\
-2
\end{bmatrix}
=
\begin{bmatrix}
0 \\
2 \\
1
\end{bmatrix}
$$

#### Example of Adding Two Vectors of Different Sizes

$$
\begin{bmatrix}
1 \\
2
\end{bmatrix}
+
\begin{bmatrix}
1 \\
2 \\
3
\end{bmatrix}
\text{is NOT defined}
$$


### Multiplication by Scalars

If $\bar{v}$ is a vector of size $n$ and $c$ is a real number, then you can multiple every value in $\bar{v}$ by $c$:

$$
c \bar{v}=
\begin{bmatrix}
cv_{1} \\
cv_{2} \\
\vdots \\
cv_{n}
\end{bmatrix}
$$

#### Multiplying Vectors as Arrows

To multiply vector $\bar{v}$ (as an arrow) by a scalar $c$, keep the direction and stretch the length by a factor of $c$. 

*Note that if $c<0$, we need to flip the direction of $\bar{v}$*.


## Comparing Directions of Vectors

Say $\bar{v}, \bar{w}$ are real, non-zero vectors.
1. They have the same direction if there is a value $c>0$ such that $\bar{v}=c \bar{w}$
2. They have the opposite direction if there is a value $c<0$ such that $\bar{v}=c \bar{w}$
3. $\bar{v}, \bar{w}$ are parallel if 1 or 2 holds

### Example

Are the following vectors parallel?

$$
\begin{bmatrix}
1 \\
2 \\
3 \\
4
\end{bmatrix} 
=
\begin{bmatrix}
2 \\
4 \\
6 \\
7
\end{bmatrix}
$$

There is no real value $c$ that linearly scales the left vector to the right vector, thus the vectors are *not* parallel.

## Linear Combinations of Vectors

We can define a linear vector by 


Then $c_{1}\bar{v_{1}} +c_{2}\bar{v_{2}}+\cdots+c_{k}\bar{v_{k}}$ is called a **linear combination** of $v_{1},v_{2},\cdots, v_{k}$ with weights $c_{1},c_{2},\cdots,c_{k}$.


## Span of a Vector

The span of a vector is the set of all possible linear combinations of the vector (think back to a [[Power Set]] from discrete math).

If $\bar{v}$ in $\mathbb{R}$
### Example of Graph

$$
\bar{v_{1}}=
\begin{bmatrix}
1 \\
2
\end{bmatrix}
$$

What is the $\text{span}(v_{1})$?

$$
=\begin{bmatrix}
c \\
2c
\end{bmatrix} : \text{ where c is any number}
$$

![[Vector Span.svg]]

The span($v_1$) is the line through $\bar{o}, \bar{v}$

### Example

$$
\bar{v_{1}}=
\begin{bmatrix}
1 \\
0 \\
0
\end{bmatrix}
\bar{v_{2}}=
\begin{bmatrix}
0 \\
1 \\
0
\end{bmatrix}
$$

$$
\begin{align}

\end{align}
$$


If $\bar{v,}$