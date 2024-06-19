Use [Basic Equivalences](Basic%20Equivalences.md) to manipulate compound propositions. ^b052a7

We can also use them to prove things:

- compound propositions are tautologies
- one compound proposition is equivalent to another

Very similar layout and process to [proofs using basic equivalences](Proofs%20Using%20Basic%20Equivalences.md).

**Example:**
$p\implies q \equiv \neg q\implies\neg p$
Contrapositive (basic equivalence)

**Start on one side and manipulate it until you hopefully end up with the other side**

Preferably start with the more complicated one.

$\neg q\implies\neg p$
$\equiv$ \<Implication Simplification>
$\neg(\neg q)\vee\neg p$
$\equiv$ \<Double Negation>
$q\vee\neg p$

Trying to get to $p\implies q$

$\equiv$ \<Commutativity>
$\neg p \vee q$
$\equiv$ \<Implication Simplification>
$p\implies q$

**Therefore, we have $p\implies q\equiv\neg q\implies\neg p$**
