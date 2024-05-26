
## Linear Transformations

Consider the following linear transformations of the variables $x$ and $y$:

$$
v=a+bx\text{ and } w=c+dy
$$

where $a,b,c,$ and $d$ are all known constants.

With Univariate data, we know:

$\bar{v}=a+b\bar{x}$
$\bar{w}=c+d\bar{x}$
$s^2_v=b^2s^2_x$
$s^2_w=d^2s^2_y$
$s_v=|b|s_x$
$s_w=|d|s_y$

With respect to the linear association between $v$ and $w$, we can show the following:

$$
s_{vw}=bds_{xy}
$$

$$
\begin{align}
   r_{vw}=\left\{
\begin{array}{ll}
      r_{xy}\text{ if b and d are both positive or both negative} \\
	      -r_{xy}\text{ if b and d are opposite signs} \\
\end{array} 
\right. 
\end{align}
$$
## Linear Combinations

With two variables, one can also consider a linear combination of the variables $x$ and $y$ as follows:

$$
v=k+ax+by
$$

where $k,a,$ and $b$ are known constants.

We can then show the following:

Sample mean of $v$: $\bar{v}=k+a\bar{x}+b\bar{y}$

Sample variance of $v$:$s^2_v=a^2s^2_x+b^2s^2_y+2abs_{xy}$

Sample standard deviation of $v$: $s_v=\sqrt{s^2_v}=\sqrt{a^2s^2_x+b^2s^2_y+2abs_{xy}}$ 