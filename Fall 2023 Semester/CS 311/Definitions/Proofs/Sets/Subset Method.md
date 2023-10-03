# Definition
A subset method proof is a type of proof meant for Sets.

Defined as

$$\overline{A\cap B}=\overline{A}\cup\overline{B}$$

To show that $\overline{A\cap B}=\overline{A}\cup\overline{B}$ , we will show that $\overline{A\cup B}\subseteq \overline{A}\cup \overline{B}\;\wedge\;\overline{A}\cup \overline{B}\subseteq \overline{A\cup B}$ 

First, we will show that

$$\overline{A\cap B}\subseteq\overline{A}\cup\overline{B}$$

$\text{let}\;x\in \overline{A\cap B}$
$\therefore$ by definition of [[Definitions#Complement|complements]], $x\notin A\cap B$ or $\neg(x\in A\cap B)$
$\therefore$ by definition of [[Definitions#Intersection|intersections]] $\neg(x\in A\wedge x\in B)$
By DeMorgan's Law, we have $\neg(x\in A)\vee\neg(x\in B)$
$\therefore$ by definition of $\notin$ and [[Definitions#Complement|complements]], we have $x\in\overline{A}\vee x\in\overline{B}$
$\therefore$ by definition of [[Definitions#Union|unions]], $x\in\overline{A}\cup\overline{B}$
$\therefore$ We have shown that $x\in\overline{A\cap B}\to x\in\overline{A}\cup\overline{B}$
$\therefore \overline{A\cap B}\subseteq\overline{A}\cup\overline{B}$ 

Next, we have to show that 

$$\overline{A}\cup \overline{B}\subseteq \overline{A\cup B}$$

$\text{let}\; x\in\overline{A}\cup\overline{B}$
$\therefore$ by definition of unions