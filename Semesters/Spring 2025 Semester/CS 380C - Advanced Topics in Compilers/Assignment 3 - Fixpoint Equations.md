### Problem 1

#### Subproblem A

Inference rules for `REACHABLE`:

$$
\begin{align} \\
\text{Start: }S\in \text{REACHABLE} \\ \\
\frac{{A\in \mathrm{REACHABLE}\;\;\; A \to \alpha \in P\;\;\;B\in \alpha\;\;\;B \in N}}{B \in \text{REACHABLE}}
\end{align}
$$


#### Subproblem B

Computing `USELESS`:

```pseudo
USELESS = {}
USEFUL = {}

// mark all the terminals, will walk backwards from here to non-terminals
for each production A -> Y1...Yn:
	if Y1...Yn consists only of terminals or is ε:
		add A to USEFUL

// add non-terminals to the useful set if we can access them from an
// already existing element in USEFUL
repeat
	still_more = false
	for each production A -> Y1...Yn
		is_useful = true
		
		if A not in USEFUL:
			if any Yi is not in N and is not in USEFUL:
				is_useful = false
			
			if is_useful:
				add A to USEFUL
				still_more = true	// updated the set so could be more
						
end repeat when still_more == false

repeat 
	for each non-terminal A in N:
		if A is not in USEFUL:
			add A to USELESS
end repeat
				
```

### Problem 2

$$
\begin{align}
3x+y=4 \\
x-2y=3
\end{align}
$$

#### Subproblem A

Initial value $(x_{1}=0,y_{1}=0)$ 

$$
\begin{align}
x=\frac{4-y}{3} \\ \\

y=\frac{x-3}{2}
\end{align}
$$

Recurrence Relation: 

$$
\begin{align}
x_{i+1}=\frac{4-y_{i}}{3} \\
 \\
y_{i+1}=\frac{x_{i}-3}{2}
\end{align}
$$
Rewritten in matrix form as
$$
\begin{pmatrix}
x_{i+1} \\
y_{i+1}
\end{pmatrix}=
\begin{pmatrix}
\frac{4-y_{i}}{3} \\
\frac{x_{i}-3}{2}
\end{pmatrix}
$$

#### Subproblem B

$$
\begin{align}
\text{Initial Condition: }
&x_{1}=0, y_{2}=0 \\
\text{Iteration 1} \\
&x_{2} = \frac{4-0}{3}=\frac{4}{3},y_{2} = \frac{0-3}{2}=-\frac{3}{2} \\
\text{Iteration 2} \\
&x_{3} = \frac{\left( 4+\frac{3}{2} \right)}{3} = \frac{\left( \frac{11}{2} \right)}{3}=\frac{11}{6},y_{3}= \frac{\left( \frac{4}{3}-3 \right)}{2} = \frac{\left( -\frac{5}{3} \right)}{2} = -\frac{5}{6} \\
\text{Iteration 3} \\
&x_{4}=\frac{\left( 4+\frac{5}{6} \right)}{3} = \frac{\left( \frac{29}{6} \right)}{3}=\frac{29}{18},y_{4}=\frac{\left( \frac{11}{6}-3 \right)}{2}=\frac{\left( -\frac{7}{6} \right)}{2}=-\frac{7}{12} \\
\text{Iteration 4} \\
&x_{5}=\frac{\left( 4+\frac{7}{12} \right)}{3}=\frac{\left( \frac{55}{12} \right)}{3}=\frac{55}{36},y_{5} = \frac{\left( \frac{29}{18}-3 \right)}{2} = \frac{\left( -\frac{25}{18} \right)}{2}= -\frac{25}{36} \\
\text{Iteration 5} \\
&x_{6}=\frac{\left( 4+\frac{25}{36} \right)}{3}=\frac{\left( \frac{169}{36} \right)}{3}=\frac{169}{108}, y_{6}=\frac{\left( \frac{55}{36}-3 \right)}{2}=\frac{\left( -\frac{53}{36} \right)}{2}=-\frac{53}{72} \\
\text{Iteration 6} \\
&x_{7}=\frac{\left( 4+\frac{53}{72} \right)}{3}=\left( \frac{\frac{341}{72}}{3} \right)=\frac{341}{216},y_{7}=\frac{\left( \frac{169}{108}-3 \right)}{2}=\frac{\left( -\frac{155}{108} \right)}{2}=-\frac{155}{216} \\
\text{Iteration 7} \\
&x_{8}=\frac{\left( 4+\frac{155}{216} \right)}{3}=\left( \frac{\frac{1019}{216}}{3} \right)=\frac{1019}{648},y_{8}=\frac{\left( \frac{341}{216}-3 \right)}{2}=\frac{\left( -\frac{307}{216} \right)}{2}=-\frac{307}{432} \\
\text{Iteration 8} \\
&x_{9}=\frac{\left( 4+\frac{307}{432} \right)}{3}=\frac{\left( \frac{2035}{432} \right)}{3}=\frac{2035}{1296},y_{9}= \frac{\left( \frac{1019}{648}-3 \right)}{2}=\frac{\left( -\frac{925}{648} \right)}{2}=-\frac{925}{1296} \\
\text{Iteration 9} \\
&x_{10}=\frac{\left( 4+\frac{925}{1296} \right)}{3}=\frac{\left( \frac{6109}{1296} \right)}{3}=\frac{6109}{3888}, \\
&y_{10}=\frac{\left( \frac{2035}{1296}-3 \right)}{2}=\frac{\left( -\frac{1853}{1296} \right)}{2}=-\frac{1853}{2592} \\
\\
\text{Iteration 10} \\
&x_{11}=\frac{\left( 4+\frac{1853}{2592} \right)}{3}=\frac{\left( \frac{12221}{2592} \right)}{3}=\frac{12221}{7776}, \\
&y_{11}=\frac{\left( \frac{6109}{3888}-3 \right)}{2}=\frac{\left( -\frac{5555}{3888} \right)}{2}=-\frac{5555}{7776}
\end{align}
$$

Geogebra Rendering of the points (x, y, iteration):
![[Pasted image 20250225011305.png]]