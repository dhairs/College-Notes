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

### Predicting the Branch Outcome

Imagine we have `C` code like the following:
```c
void foo() {
	for(int i = 0; i < 5; i++) {
		...
	}
}
```

Simplified assembly can be described as:
```asm
.foo:
	mov r0, 0
.loop:	
	cmp r0, 5
	beq .exit
	add r0, r0, 1
	bne .loop
.exit:
	NOP
```

The loop is the critical path and most of the time will be predicted not taken. We will use a simple bimodal predictor. 

If we use a single-bit predictor, we remember the **last outcome**, and the **current prediction** becomes the last outcome.

![[Branch Predictor Bimodal.png]]

The misprediction rate is $\frac{1}{6}$ for the first call to `foo` and $\frac{2}{6}$ for the second and onwards.

#### Improving Accuracy

We can always add extra bits to the table. 

The `beq` instruction in `foo` is fundamentally biased towards *not taken*
- One exception at loop exit shouldn't impact this tendency significantly
- Add **hysteresis**

Use a **saturating counter**, increment when taken, decrement when not taken.

![[BP Saturating Counter.png]]

We can predict not taken when we have `00` or `01`, and predict taken when we have `10` or `11`.

This is a Moore finite state machine. We start from `01` and the misprediction rate eventually decreases to $\frac{1}{6}$.

![[BP Saturating Counter with Logic.png]]

#### Global History

We need to have a shift register that records the history of the last $k$ branches encountered by the processor.

We have one bit for each branch, regardless of the PC. We record `1` for branch taken and `0` for branch not taken.

Consider a 2-bit **global history register** (GHR) like this:

![[BP GHR.png]]
We have two conditional branches in the running example: `beq .exit` and `bne .inc` 

Use both $k$ bits of the GHR and least-significant $n$ bits of the PC to index into the **pattern history table** (PHT). The PHT has $2^{n+k}$ entries and increased accuracy.

This is also called a **GAp two-level adaptive predictor**: G for Global, A for Adaptive, p for per-branch/pc.

Invented by UT professor Yale Patt! [Yeh & Patt 1991](https://www.inf.pucrs.br/~calazans/graduate/SDAC/saltos.pdf).

> [!FAQ] Bits used by different configurations
> GAp: $k + w\times {2}^k\times 2^n$
> GAg: $k + w \times 2^k$
> PAg: $k\times 2^n+w\times 2^k$
> 
