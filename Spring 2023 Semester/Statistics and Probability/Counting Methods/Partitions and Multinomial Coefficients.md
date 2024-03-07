## Definition

Suppose we have an $n$-element set which can be partitioned into $r$ disjoint subsets, with the $i$-th subset containing $n$ elements

This is similar to having $n$ objects, of which $n_1$ are alike $n_2$ are alike $\ldots n_r$ are alike.

The number of permutations of the $n$-element set to form this configuration is given by:

$$
\frac{n!}{n_1!n_2!\ldots n_r!}
$$

These are also called **multinomial coefficients**

### Ex: Signals

How many different signals, each consisting of 9 flags hung in a line, can be made from a set of 4 white flags, 3 red flags, and 2 blue flags, if all flags of the same color are identical?

Answer:

$$
\frac{9!}{4!3!2!}=1260
$$

## Occupancy Problems (Boxes and Objects)
### Distinguishable Objects and Distinguishable Boxes

The number of ways of distributing $n$ distinguishable objects into $r$ distinguishable boxes so that $n_i$ objects are placed into box $i$, for $i=1,2,\ldots,r$ is:

$$
\Bigl({{n} \atop {n_1,n_2,\ldots,n_r} } \Bigl)\, = \frac{n!}{n_1!n_2!\ldots n_r!}
$$

### Indistinguishable Objects and Distinguishable Boxes

#### Every box gets an object
Suppose we want to distribute $n$ indistinguishable objects into $k$ boxes so that *every box gets at least one object*

If $x_i$ is the number of objects going into box $i$, we are looking for the number of solutions to:

$$
x_1+x_2+\ldots+x_k=n, \text{where } x_i>0 
$$

If we express this as bars and stars, you want to place $k-1$ bars in $n-1$ spaces, so this can be expressed as:

$$
\Bigl({{n-1}\atop{k-1}}  \Bigl)
$$

This is just regular [[Permutations and Combinations#Combinations|combinations]].
#### Not every box gets an object
Suppose we want to distribute $n$ indistinguishable objects into $k$ boxes so that every box *may or may not get an object*

If $x_i$ is the number of objects going into box $i$, we are looking for the number of solutions as the sum of $k$ non-negative integers:

$$
x_1+x_2+\ldots+x_k=n, \text{where } x_i\geq0 
$$

The number of ways we can do this can be expressed as:

$$
\Bigl( {{n+k-1}\atop{k-1}} \Bigl)
$$
