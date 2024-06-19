## What is a Clock?

A clock is a free running **binary** signal that constantly switches between 0 and 1 on a fixed cycle time. This is representable as a square wave. 

![[Clock Square Wave.svg|500]]

> [!NOTE] LaTeX
> ```tikz
\usepackage{pgfplots}
\pgfplotsset{compat=1.16}
\begin{document}
\begin{tikzpicture}
\begin{axis}[
width=10cm,
height=4cm,
x axis line style={-stealth},
y axis line style={-stealth},
title={Square wave},
xticklabels={},
ymax = 1.5,xmax=7.5,
axis lines*=center,
ytick={0.5,1},
xlabel={Time $\rightarrow$},
ylabel={Amplitude},
xlabel near ticks,
ylabel near ticks]
\addplot+[thick,mark=none,const plot]
coordinates
{(0,0) (0,1) (1,0) (2,1) (3,0) (4,1) (5,0) (6,1) (7,0)};
\end{axis}
\end{tikzpicture}
\end{document}```

**Rising Edge**: When the clock transitions from $0\to1$.

**Falling Edge**: When the clock transitions from $1\to0$.

**Clock Cycle**: The time interval $T$ between successive rising *or* falling edges, this is measured in seconds

**Clock Frequency**: Reciprocal of the clock cycle, $f=\frac{1}{T}$, this is measured in hertz (Hz)
