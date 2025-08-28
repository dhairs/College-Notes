
## Impulse Response

$y(s)=x(s)G(s)$. Here, $x(s)=1$

$$
\begin{align}
Y_{1}(s)=\frac{2}{(s+1)(s+2)}=\frac{k_{1}}{(s+1)}+\frac{k_{2}}{(s+2)} \\
k_{1}=\frac{2}{s+2}|_{s=-1}=2 \\
k_{2}=\frac{2}{s+1}|_{s=-2}=-2 \\
Y_{1}(s)=\frac{2}{s+1}-\frac{2}{s+2} \\ \\
\boxed{y_{1}(t)=h_{1}(t)=2(e^{-t}-e^{-2t})*1(t)}
\end{align}
$$
Note that in step 4, we used the Laplace transform of $\frac{1}{s+a}$, which is $e^{-at}$.

When you have poles, the pole that is closer to the origin without going over (e.g. without making it unstable), will persist longer in time domain response than the other terms.

So in this case, we just look at the slowest decay and estimate the steady state to be arrived when we reach 5x the time constant. In this case, that's ~5s because $s=1$ and $\tau=1$.

$$
\begin{align}
Y_{2}(s)=\frac{2}{(s+1)^2+1^2}=s\left[ \frac{1}{(s+1)^2+1^2} \right] \\
\text{This looks like one of our standard Laplace transforms, we just need to rearrange.} \\
\boxed{y_{2}(t)=2e^{-t}\sin t\cdot 1(t)}
\end{align}
$$


<iframe src="https://www.desmos.com/calculator/9n5ib5ofmm?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

## Step Responses

Computing step responses, $x(s)=\frac{1}{s}$

$$
\begin{align}
Y_{1}(s)=x(s)G_{1}(s)=\frac{1}{s} \frac{2}{(s+1)(s+2)} \\
Y_{1}(s) = \frac{k_{1}}{s} + \frac{k_{2}}{s+1}+\frac{k_{3}}{s+2} \\
 \\
k_{1}=\frac{2}{(s+1)(s+2)}|_{s=0}=1
\end{align}
$$

$$
\begin{align}
y_{2}(s)=x(s)G_{2}(s) \\
y_{2}(s)=\frac{1}{s} \frac{2}{s^2+2s+2}=\frac{A}{s}+\frac{Bs+c}{s^2+2s+2} \\
 \\
\text{Find A in the "normal manner"} \\
A=\frac{2}{s^2+2s+2}|_{s=0}=1 \\
\text{Replace A, now} \\
y_{2}(s)=\frac{2}{s(s^2+2s+2)}=\frac{1}{s} + \frac{Bs+c}{s^2+2s+2} \\
\text{Cross multiply over common denominator and equate numerator} \\
(0s^2+0s)+2=(s^2+2s+2)+Bs^2+cs \\
2=(1+B)s^2+(2+c)s+2
\end{align}
$$

Eventually we get:

$$
\begin{align}
y_{2}(s)=\frac{1}{s}-\left[ \frac{s+1}{(s+1)^2+1^2} + \frac{1}{(s+1)^2+1^2} \right]
\end{align}
$$

And then we can perform reverse Laplace and find that:

$$
y_{2}(t)=[1-e^{-t}]
$$