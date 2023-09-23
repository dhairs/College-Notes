---
aliases:
  - CS 311 HW 1
---

#### Problem 1

a. $(b\wedge \neg c)\to a$
b. $\neg c \to a$
c. $a \leftrightarrow\neg c$

#### Problem 2

let $s =$ "The system is in multiuser state"
let $o =$ "The system operating normally"
let $i$ = "The system is in interrupt mode"
let $k$ = "The kernel is functioning"

In propositional form:

1.  $s \leftrightarrow o$
2.  $o\to k$
3.  $\neg k\vee i$
4.  $\neg s\to i$
5.  $\neg i$
    Since we know the $\neg i$, $i \equiv F$

Since $\neg s\to i$, $\neg s$ MUST be false. As a result, $s\equiv T$

Since $s\leftrightarrow o$ and $s\equiv T$, we know that $o$ MUST be true as well. As a result, $o\equiv T$

Since $o\equiv T$ and $o\to k$, $k$ MUST be true as well. As a result, $k\equiv T$

Since $k\equiv T$, and $\neg k\vee i$, $i$ MUST be true. As a result, $i\equiv T$.

However, this is a contradiction, because one of our premises is $\neg i$, so **the system is not consistent.**

#### Problem 3

##### a.

| $p$ | $q$ | $r$ | $p\to q$ | $p\to r$ | $q\vee r$ | $p\to(q\vee r)$ | $p\to q\vee p\to r$ |
| --- | --- | --- | -------- | -------- | --------- | --------------- | ------------------- |
| T   | T   | T   | T        | T        | T         | T               | T                   |
| T   | T   | F   | T        | F        | T         | T               | T                   |
| T   | F   | T   | F        | T        | T         | T               | T                   |
| T   | F   | F   | F        | F        | F         | F               | F                   |
| F   | T   | T   | T        | T        | T         | T               | T                   |
| F   | T   | F   | T        | T        | T         | T               | T                   |
| F   | F   | F   | T        | T        | F         | T               | T                   |
| F   | F   | T   | T        | T        | T         | T               | T                   |

**Because both $p\to(q\vee r)$ and $p\to q\vee p\to r$ columns in the proof table have the same values, both compound propositions are equivalent.**

##### b.

| $p$ | $q$ | $\neg q$ | $p\vee q$ | $(p\vee q)\to \neg q$ | $\neg((p\vee q)\to\neg q)$ |
| --- | --- | -------- | --------- | --------------------- | -------------------------- |
| T   | T   | F        | T         | F                     | T                          |
| T   | F   | T        | T         | T                     | F                          |
| F   | T   | F        | T         | F                     | T                          |
| F   | F   | T        | F         | T                     | F                          |

**Because the columns for both $q$ and $\neg((p\vee q)\to\neg q)$ have the same truth values for every truth value of $p$ and $q$, both propositions are equivalent.**

#### Problem 4

##### a. Prove $(p\to q)\vee (q\to r)$

$(p\to q)\vee (q\to r)$
$\equiv$ \<Implication Simplification>
$(\neg p \vee q) \vee(\neg q\vee r)$
$\equiv$ \<Associative Laws>
$(\neg p \vee (q\vee\neg q))\vee r$
$\equiv$ \<Excluded Middle>
$(\neg p \vee T) \vee r$
$\equiv$ \<Domination Laws>
$T\vee r$
$\equiv$ \<Domination Laws>
$T$
$\therefore$ the proposition is a Tautology

##### b. Prove $\neg(\neg(p\wedge q)\to (p\to \neg q))$

$\neg(\neg(p\wedge q)\to (p\to \neg q))$
$\equiv$ \<DeMorgan's Laws>
$\neg((\neg p\vee\neg q)\to (p\to \neg q))$
$\equiv$ \<Implication Simplification>
$\neg((\neg p\vee\neg q)\to (\neg p\vee\neg q))$
$\equiv$ \<Implication Simplification>
$\neg(\neg(\neg p\vee \neg q)\vee(\neg p\vee \neg q))$
$\equiv$ \<DeMorgan's & Double Negation>
$\neg((p\wedge q)\vee (\neg p\vee \neg q))$
$\equiv$ \<DeMorgan's & Double Negation>
$\neg(p\vee q)\wedge ( p\wedge q)$
$\equiv$ \<Contradiction>
$F$
$\therefore$ the proposition is a contradiction.

##### c. Prove $((\neg p\vee q)\to q)$

$((\neg p\vee q)\to q)$
$\equiv$ \<Implication Simplification>
$(\neg(\neg p\vee q)\vee q)$
$\equiv$ \<DeMorgan's Law & Double Negation>
$(p\wedge\neg q)\vee q$
$\equiv$ \<Distributive Laws>
$(p\vee q)\wedge(q\vee\neg q)$
$\equiv$ \<Excluded Middle>
$(p\vee q)\wedge T$
$\equiv$ \<Identity Laws>
$p\vee q$
$\therefore$ the proposition is a **contingency** because the truth value is based on the values of both $p$ and $q$.

#### Problem 5

##### Prove $((p\vee q)\wedge (\neg p\vee r))\to (q\vee r)$

$((p\vee q)\wedge (\neg p\vee r))\to (q\vee r)$
$\equiv$ \<Implication Simplification>
$\neg((p\vee q)\wedge (\neg p\vee r))\vee(q\vee r)$
$\equiv$ \<DeMorgan's Laws>
$(\neg(p\vee q)\vee \neg(\neg p\vee r))\vee(q\vee r)$
$\equiv$ \<DeMorgan's Laws & Double Negation>
$((\neg p\wedge\neg q)\vee (p\wedge\neg r))\vee(q\vee r)$
$\equiv$ \<Associative Laws>
$((\neg p\wedge\neg q)\vee (p\wedge\neg r)\vee q)\vee r$
$\equiv$ \<Associative and Commutative Laws>
$(((\neg p\wedge\neg q)\vee(q\vee(p\wedge\neg r)))\vee r$
$\equiv$ \<Associative Laws>
$(((\neg p\wedge \neg q)\vee q)\vee(p\wedge\neg r))\vee r$
$\equiv$ \<Associative Laws>
$((\neg p\wedge \neg q)\vee q)\vee((p\wedge\neg r)\vee r)$
$\equiv$ \<Distributive Laws x2>
$((\neg p\vee \neg q)\wedge(q\vee q))\vee((p\vee r)\wedge(r\vee\neg r))$
$\equiv$ \<Idempotent Laws & Excluded Middle>
$((\neg p\vee q)\wedge T)\vee((p\vee r)\wedge T)$
$\equiv$ \<Identity Laws x2>
$(\neg p\vee q)\vee (p\vee r)$
$\equiv$ \<Associative Laws>
$((\neg p\vee q)\vee p)\vee r$
$\equiv$ \<Associative Laws>
$(\neg p\vee (q\vee p))\vee r$
$\equiv$ \<Commutative Laws>
$(\neg p\vee (p\vee q))\vee r$
$\equiv$ \<Associative Laws>
$((\neg p\vee p)\vee q)\vee r$
$\equiv$ \<Excluded Middle>
$(T\vee q)\vee r$
$\equiv$ \<Domination Laws>
$T\vee r$
$\equiv$ \<Domination Laws>
$T$
$\therefore$ the proposition is a tautology.
