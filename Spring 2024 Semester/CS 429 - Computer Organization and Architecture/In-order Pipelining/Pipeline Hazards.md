## Dependences

unfinished notes on dependences

---

## Hazards

**Implementation Hazards** (often "pipeline hazards" or "hazard") are _boolean-valued_ functions of an [[Instruction Set Architectures|ISA]] implementation $L$ and an instruction sequence $S=[I_1,\ldots, I_n]$, with $I_1\to I_n$.

- A hazard value of _True_ (a hazard _is_ present) indicates that implementation $L$ does not refine IaaT semantics for $S$, and that $S$ is a counterexample/witness to this fact
- A hazard value of _False_ (a hazard is _absent_) indicates that the implementation $L$ does refine IaaT semantics for $S$

We classify pipeline hazards as data hazards or control hazards

The presence of a dependence may result in hazards for a given implementation.

**We don't want hazards.**

### Sources of Hazards

Those components of machine state that _are read in an earlier stage of the pipeline and written in a later stage of the pipeline_ can result in a hazard **if the respective instructions are not separated sufficiently in time**.

- 5 cycles of separation are guaranteed to be sufficient to prevent a dependence turning to a hazard in PIPE-

Certain components of machine state can cause hazards:

- PC: Control hazard (read by F; written by F, X, M)
- Architectural registers: Data hazard (read by D; Written by W)

Certain components can _not_ cause hazards:

- Data memory: Read _and_ written by M
- Condition codes: Read _and_ written by X

## Preventing Hazards

We can't allow program dependencies to turn into pipeline hazards

Therefore, we need to find ways of changing the pipeline data and control paths to make the final design (PIPE) remain faithful to IaaT semantics. We **must** be correct, this can come at the cost of sacrificing performance. If we have two correct implementations, we pick the one that sacrifices less performance.

Solutions will be described in terms of "policies" and "mechanisms"

3 situations to deal with:

- data dependence - earlier writes, later reads, insufficient space between to be safe
- program counter messed up - mispredicted conditional branch
- return - have to use x30

### Policy: Stalling for Data Hazards

Suppose we have a data hazard at this cycle in the pipeline between instructions $i$ and $j$ with $i {d\atop{\to}}j$ .

The presence of a data hazard means that $i$ will write a value that $j$ needs to read, but it hasn't been written _yet_.

- Basically: $j$ is in D, but $i$ hasn't reached W and completed the write to the register file (the write is **pending**)
- If $i$ is a computational instruction, (i.e., the value is generated in X), the scenario is called a "**def-use hazard**"
- If $i$ is a load instruction (i.e., the value is generated in M), the scenario is called a "**load-use hazard**"

#### Our Solution

Let the instructions ahead of $j$, including $i$, proceed to completion, while holding back ("**stalling**") $j$ and any instructions after it.

Once $i$ completes the write, allow $j$ and any instructions after it to proceed

This is called **pipeline control**.

#### Considerations for Stalling

The pipeline is synchronous — so we need to keep every pipeline stage busy at each clock cycle, doing something that won't mess things up further.

- This is perfect for the `nop` instruction

How can we insert it?

- The mechanism for "inserting `nop`s" is called **bubble insertion**.
- We will call inserting the `nop` "inserting a bubble".
- We may need to repeat the bubble for multiple cycles

Detecting that a data dependence of the program is about to turn into a data hazard in the pipeline and taking the necessary coordinated action across all the pipeline stages to prevent this from happening is called **pipeline control**.

- This requires that we have a global view of the entire pipeline so that we can decide what the view needs to be on **the next cycle** so we can ensure correct behavior and take necessary action to set up the correct global view

### Policy: Squashing for `B.cond` Control Hazard

Our branch prediction strategy is Predict Taken

- If our prediction is incorrect, we discover this only at the end of the cycle where the `B.cond` instruction is in X
- By this time, two more instructions are already in the pipeline, in F and D
- These two instructions shouldn't have been in the pipeline in the first place (because we picked up the wrong branch)
- So we can just remove them from the pipeline
  - Especially good because they haven't updated any architectural state yet
- Instructions must be fetched starting at the sequential successor of the `B.cond`

This strategy is called **cancellation/squashing**.

Our mechanism will once again be **bubble insertion**, we'll insert two bubbles in the D and X stages.

Detecting that a control dependence is about to turn into a control hazard and taking necessary actions to prevent this from happening is the job of the **pipeline control**.

### Policy: Stalling for `ret` Control Hazard

With `ret`, we have no clue what the next instruction is, because it is an arbitrary memory location. We won't know the address until `ret` has retrieved the Return Address from register X30 at the end of the next cycle.

Let's just not insert anything for the cycle.

This strategy is once again **stalling**.

Our mechanism is once again **bubble insertion**, where we insert a singular bubble at F

Detecting this control dependence is about to turn into a control hazard and taking the necessary action to prevent it is the job of the **pipeline control**.

## Control Signals for Pipeline Control
