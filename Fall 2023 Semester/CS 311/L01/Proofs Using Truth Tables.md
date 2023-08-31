Remember that to prove a theorem, we need to show that a statement of the following form is a tautology:
![[What is a Proof?#^45a1e8]]

We can use [[Truth Tables|truth tables]] to show that these premises are true, and therefore our conclusion is true as our proof. ^d6ec52

**Example:** 
"John or Mary must drive me to the store. If John drives me to the store, John will be late for work. John cannot be late for work. Therefore, Mary must drive me to the store."

$J$: John drives me to the store.
$M$: Mary drives me to the store
$L$: John is late for work

Rewritten with these [[Boolean and Propositional Logic#^20fbeb|variables]]:
$J\vee M$ ... $J\implies L$ ... $\neg L$, therefore $M$

$(J\vee M)\wedge (J\implies L)\wedge (\neg L) \implies M$
