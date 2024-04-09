
## Dependences

--- 

--- 

## Hazards

**Implementation Hazards** (often "pipeline hazards" or "hazard") are *boolean-valued* functions of an [[Instruction Set Architectures|ISA]] implementation $L$ and an instruction sequence $S=[I_1,\ldots, I_n]$, with $I_1\to I_n$.

- A hazard value of *True* (a hazard *is* present) indicates that implementation $L$ does not refine IaaT semantics for $S$, and that $S$ is a counterexample/witness to this fact
- A hazard value of *False* (a hazard is *absent*) indicates that the implementation $L$ does refine IaaT semantics for $S$ 

We classify pipeline hazards as data hazards or control hazards 

The presence of a dependence may result in hazards for a given implementation.

**We don't want hazards.**

### Sources of Hazards

Those components of machine state that *are read in an earlier stage of the pipeline and written in a later stage of the pipeline* can result in a hazard **if the respective instructions are not separated sufficiently in time**.
- 5 cycles of separation are guaranteed to be sufficient to prevent a dependence turning to a hazard in PIPE-

Certain components of machine state can cause hazards:
- PC: Control hazard (read by F; written by F, X, M)
- Architectural registers: Data hazard (read by D; Written by W)

Certain components can *not* cause hazards:
- Data memory: Read *and* written by M
- Condition codes: Read *and* written by X

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

The presence of a data hazard means that $i$ will write a value that $j$ needs to read, but it hasn't been written *yet*.
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