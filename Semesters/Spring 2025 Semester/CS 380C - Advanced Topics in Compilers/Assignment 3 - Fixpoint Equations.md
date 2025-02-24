
1a)
$$
\begin{align} \\
\text{Start: }S\in \text{REACHABLE} \\ \\
\frac{{A\in \mathrm{REACHABLE}\;\;\; A \to \alpha \in P\;\;\;B\in \alpha\;\;\;B \in N}}{B \in \text{REACHABLE}}
\end{align}
$$

1b)

Computing USELESS:

```pseudo
USELESS = {}
USEFUL = {}

repeat until keep_going = false
	keep_going = false
	for each production A -> Y1...Yn
		if A not in USEFUL:
			is_useful = true
			
			if Y1...Yn are all non-terminal and any are not in USEFUL:
				is_useful = false
			
			if is_useful:
				add A to USEFUL
				keep_going = true
		
				
```