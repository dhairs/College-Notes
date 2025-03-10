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

### Leveraging Local and Global Information

The previous predictors used a ton of data and state to be able to predict branches. We can, however, just use a simple XOR with shared indexes into a prediction table. Eventually, a bunch of addresses and behaviors will converge into a behavior and be placed at a certain index in the table which will then be trained onto local history. Called the "gshare" predictor.

![[gshare.png]]

There are also combining or "tournament" predictors used in Alpha 21264.

![[tournament predictor.png]]

### Tagged Hybrid Predictors

Stands for **TA**gged **GE**ometric predictor (TAGE). It keeps multiple predictions with different history lengths: $L(i)=[a^{i-1}\times L(1)+0.5]$. The hash function can once again just be an XOR. It partially tags predictions to avoid false matches and only provides a prediction on match.


| ![[TAGE Predictor.png]]                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------- |
| https://www.researchgate.net/figure/The-TAGE-Predictor-with-N-Tagged-Tables-organization-of-the-TAGE-predictor-It-consists_fig1_254023355 |

### Neural Branch Predictor

Invented by UT Student and Professor Calvin Lin! [Jiménez & Lin 2002](https://dl.acm.org/doi/abs/10.1145/571637.571639).

The algorithm is to hash the branch address to produce an index $i\in[0,N-1]$ into the table of perceptrons. Fetch perceptron $i$ from the table into a vector register $P_{0:n}$ of weights $\{w_{i}\}$. Compute $y$ as the dot product of $P$ and the global branch history register (BHR). BHR is encoded as 1 for a branch that is taken and -1 for a branch that is not taken. Predict branch as `not taken` of $y<0$ and `taken` otherwise. Once the branch is resolved, use the training algorithm to update the weights in $P$. Write back the updated $P$ into entry $i$ of the table of perceptrons.

The **dot product** is the slowest/hardest operation so we need to optimize it. To approximate the dot product, we will make the weights $w_{i}$ small-width integers because we don't need insane accuracy. Since BHR entries are conceptually $\pm 1$, we just need to add to $w_{i}$ if it is 1 and subtract if -1. For subtraction we just use $-w_{i}\approx  \bar{w_{i}}$. Since we only need the sign bit to predict, the other bits can be computed slower.

The **training algorithm** takes in 3 inputs: $y,t,\theta$ where $t$ is the branch outcome and $\theta$ is a training threshold parameter (hyperparameter). If $\text{sgn}(y)\neq t\text{ or }|y|\leq 0$ then `forall` $i\in [0,n]:w_{i} \leftarrow w_{i}+t \cdot x_{i}$. Empirically, the best threshold $\theta$ for a given history length $h$ is $\theta=\lfloor 1.93h+14 \rfloor$.


### Predicting the Branch Target
