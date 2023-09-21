### Definition
$(p_1\vee p_2\vee\ldots\vee p_n)\to q\equiv(p_1\to q)\wedge(p_2\to q)\wedge\ldots(p_n\to q)$


the original conditional statement wtih a hypothesis made up of a disjunction of propositions $p_1, p_2,\ldots,p_n$ can be proved by proving each of the $n$ conditional statements $p_i\to q$ individually.

To prove $p\to q$, we can find $$p_1\vee p_2\vee\ldots\vee p_n\equiv p$$ and then individually prove every case.

### Example: Use proof by cases to prove that $|xy|=|x||y|$, where $x$ and $y$ are real numbers.

First, we need the definition of absolute value.
![[Definitions#Absolute Value]]

#### Proof: We will consider four cases.

1. $x≥0, y≥0$
2. $x≤0, y≥0$
3. $x≥0, y≤0$
4. $x≤0, y≤0$

#### Case 1: $x≥0, y≥0$. 
Therefore, we have $|x| = x$ and $|y| = y$.
Also, $xy≥0$. Therefore,

$$\begin{align}
|xy|
\\\equiv<definition>
\\x*y
\\\equiv<substitution>
\\|x||y|
\end{align}$$
$\therefore$ for $x≥0, y≥0$, $|xy|=|x||y|$

#### Case 2: $x≤0, y≥0$. 
Therefore, we have $|x| = -x$ and $|y| = y$.
Also, $xy≤0$. Therefore,
$$\begin{align}
|xy|
\\\equiv<definition>
\\(-x)*y
\\\equiv<substitution>
\\|x||y|
\end{align}$$
$\therefore$ for $x≤0, y≥0$, we have $|xy|=|x||y|$

#### Case 3: $x≥0, y≤0$. 
Therefore, we have $|x| = x$ and $|y| = -y$.
Also, $xy≤0$. Therefore,
$$\begin{align}
|xy|
\\\equiv<definition>
\\ x*(-y)
\\\equiv<substitution>
\\|x||y|
\end{align}$$
$\therefore$ for $x≥0, y≤0$, we have $|xy|=|x||y|$

#### Case 4: $x≤0, y≤0$. 
Therefore, we have $|x| = -x$ and $|y| = -y$.
Also, $xy≥0$. Therefore,
$$\begin{align}
|xy|
\\\equiv<definition>
\\ (-x)*(-y)
\\\equiv<substitution>
\\|x||y|
\end{align}$$
$\therefore$ for $x≤0, y≤0$, we have $|xy|=|x||y|$


$\therefore$ for all real numbers, $x$, $y$: $|xy|=|x||y|$


## Without loss of generality (WLOG)
- in the last example, we dismissed case 3 because it was the same as case 2 with reversed roles
- to shorten the proofs, we could have proved cases 2 and 3 together because both are completely arbitrary, and whichever one is positive and whichever one is even does not matter

### Example: Show that if $x$ and $y$ are integers and both $xy$ and $x+y$ are even, then both $x$ and $y$ are even.

Techniques Employed:
- [[Direct Proof by Contraposition]]
- Without loss of Generality (WLOG)
- Proof by cases

#### Proof: Using proof by contrapositive, we will show that if $x$ is odd or $y$ is odd, $x+y$ is odd or $xy$ is odd.

Without loss of generality, assume $x$ is odd.

$\therefore$ there exists and integer $m$ such that $x=2m+1$

Now, all we have to analyze is when $y$ is odd and $y$ is even.

$\therefore$ we must consider two cases, $y$ is odd or $y$ is even
##### Cases:
1. $y$ is odd
2. $y$ is even
##### Case 1: $y$ is odd.
$\therefore$ there exists integer $n$, $y=2n+1$

Now $$\begin{align}
xy\\
\equiv<substitution>\\
(2m+1)(2n+1)\\
\equiv<algebra>\\
4mn+2m+2n+1\\
\equiv<algebra>\\
2(2mn+m+n)+1\\
\end{align}$$
Since $m$ and $n$ are integers, $2mn+m+n$ is also an integer.
$\therefore$ $xy$ is odd.

##### Case 2: $y$ is even.
$\therefore$ there exists integer $n$ such that y=$2n$

Now, $$\begin{align}
x+y\\
\equiv<substitution>\\
2m+1+2n\\
\equiv<algebra>\\
2(m+n)+1
\end{align}$$$m, n$ are integers.  $\therefore$ $m+n$ is an integer.

$\therefore x+y$ is odd.

$\therefore$ By contraposition, if $xy$ and $x+y$ are even, then both $x$ and $y$ are even.