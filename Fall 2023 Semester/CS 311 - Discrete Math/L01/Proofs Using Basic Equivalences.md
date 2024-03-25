We can use the [[Basic Equivalences|basic equivalences]] to develop proofs as an alternative to using truth tables.

_Note:_ Always place your performed equivalence on a new line, with the name of the equivalence in sideways carrots (<>)

**Example:**
Starting with $(p\wedge q)\implies p$

$\equiv$ \<Implication Simp>

$\neg(p\wedge q)\vee p$

$\equiv$ \<DeMorgan's>

$(\neg p\vee\neg q)\vee p$

$\equiv$ \<Associative Law>

$\neg p\vee (\neg q\vee p)$

$\equiv$ \<Commutative>

$\neg p\vee(p\vee\neg q)$

$\equiv$ \<Associative>

$(\neg p\vee p)\vee\neg q$

$\equiv$ \<Excluded Middle>

T $\vee\neg q$

$\equiv$ \<Domination>

$T$

[[Discrete Math Terminology#^502eb0|Tautology]]
