```tikz
\usepackage{pgfplots}
\pgfplotsset{compat=1.12}

\begin{document}
\begin{tikzpicture}
\begin{axis}[
    trig format plots=rad,
    axis equal,
    hide axis
]
\addplot [domain=0:2*pi, samples=50, black] ({4*sin(x)}, {4*cos(x)});
\addplot [domain=0:2*pi,samples=200, red]({(4+sin(12*x))*sin(x)},{(4+sin(12*x))*cos(x)});
\end{axis}
\end{tikzpicture}
\end{document}
```

```tikz
\usepackage{chemfig} \begin{document} \definesubmol\fragment1{     (-[:#1,0.85,,,draw=none]     -[::126]-[::-54](=_#(2pt,2pt)[::180])     -[::-70](-[::-56.2,1.07]=^#(2pt,2pt)[::180,1.07])     -[::110,0.6](-[::-148,0.60](=^[::180,0.35])-[::-18,1.1])     -[::50,1.1](-[::18,0.60]=_[::180,0.35])     -[::50,0.6]     -[::110])     } \chemfig{ !\fragment{18} !\fragment{90} !\fragment{162} !\fragment{234} !\fragment{306} }  \end{document}
```
```tikz
\usepackage{pgfplots}

\begin{document}
\begin{tikzpicture}
\begin{axis}[
    trig format plots=rad,
    axis equal,
    hide axis
]
\addplot [domain=0:2*pi, samples=50, black] ({3(cos(x))^3(-sin(t))}, {4*cos(x)});
\addplot [domain=0:2*pi,samples=200, red]({(4+sin(12*x))*sin(x)},{(4+sin(12*x))*cos(x)});
\end{axis}
\end{tikzpicture}
\end{document}
```

