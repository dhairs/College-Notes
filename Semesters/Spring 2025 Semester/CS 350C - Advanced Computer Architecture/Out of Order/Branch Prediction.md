## Problems

In reality, there are three subproblems to this:
- Predicting the **instruction *type***: is this instruction a branch (i.e., can it cause non-sequential control transfer)?
	- Yes: {B, BR, B.cond, BL, BLR, RET}; no: everything else in ISA
- Predicting the **branch *outcome***: If the instruction is a branch, will it be taken or not?
	- Unconditionally taken: {B, BR, BL, BLR, RET}; conditionally taken: {B.cond}
- Predicting the **branch *target***: If the branch is taken, to which non-sequential address will it transfer control?
	- Statically known: {B, BL, B.cond}; dynamic: {BR, BLR, RET}

We need to make relevant predictions based solely on PC value and **prior knowledge**.

What we want to do is gather information from what happened before.

![[Branch Predictor Basic.png]]

### Predicting Instruction Type

Observation: the type of the instruction at a program counter (PC) is static

Implication: maintain a lookup table (the **Instruction Status Table**, or IST) to record and look up this information.

There are some considerations of this: size of the table, taking advantage of instruction alignment, keeping additional information in IST, aliasing between instructions.