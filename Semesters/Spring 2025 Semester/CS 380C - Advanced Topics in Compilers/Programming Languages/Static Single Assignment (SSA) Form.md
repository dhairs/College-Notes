## Definition

Static Single Assignment (SSA) is an intermediate representation of a program in which every use of a variable is reached by **exactly** one definition.

Most programs do not satisfy this condition.

It requires inserting dummy assignments called $\Phi$-functions at merge points in the [[Control Flow Graphs|CFG]] to "merge" multiple definitions

Simple algorithm: insert $\Phi$-functions for all variables at all merge points in the CFG and rename each real and dummy assignment of a variable uniquely.