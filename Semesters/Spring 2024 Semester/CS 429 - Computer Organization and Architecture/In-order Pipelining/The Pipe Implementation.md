## Data Hazards

Recall our [[Pipeline Hazards#Policy Stalling for Data Hazards|stalling policy]] for Data Hazards. This works as a general strategy, but it's not great for performance.

Why isn't it best for performance?

- The **values** that are needed by the dependent instruction are often available in pipeline registers before they're placed in the locations from where they are retrieved

What if?

- We bypass waiting for the register updates and hand off the correct bit values to allow the dependent instruction to move forward

The cost of this?

- More wires, logic, etc. (hardware)

Benefits?

- Correctness with a lower performance hit

Enter **forwarding**

## Value Forwarding

Policy: Value forwarding (aka "forwarding" or "register forwarding" or "bypassing")

Mechanism: Logic, wires

- Focus on data dependences carried through architectural registers
- Forwarding happens completely in the data path, without any involvement of the pipeline control

The idea is to transmit the bits of $R_{ij}$ over wires during a single cycle

- _from_ instruction $i$: from the end of the combinational logic block in the X stage, equivalent to `M_in`, or from `M_out`, or from `W->in`, or from `W->out`
- _to_ intercept instruction $j$: at the end of the combinational logic block in the D stage, just after incorrect values have been read for the registers
- _so_ that the correct bits are presented at the _clock's edge_ to be latched into the X pipeline register, ready for the next cycle

### Def-Use Hazard $I1{d\atop{\to}}I2$ With Forwarding

| Cycle | Instruction in | F    | D    | X    | M    | W    |
| ----- | -------------- | ---- | ---- | ---- | ---- | ---- |
| 1     | `I1`           | `I1` |      |      |      |      |
| 2     | `I2`           | `I2` | `I1` |      |      |      |
| 3     |                |      | `I2` | `I1` |      |      |
| 4     |                |      |      | `I2` | `I1` |      |
| 5     |                |      |      |      | `I2` | `I1` |
| 6     |                |      |      |      |      | `I2` |

Would have lost 3 cycles in this case without using forwarding (the dependent instruction is separated by 0 instructions, so 3 - 0 = 3)

| Cycle | Instruction in | F    | D    | X    | M    | W    |
| ----- | -------------- | ---- | ---- | ---- | ---- | ---- |
| 1     | `I1`           | `I1` |      |      |      |      |
| 2     | `N1`           | `N1` | `I1` |      |      |      |
| 3     | `I2`           | `I2` | `N1` | `I1` |      |      |
| 4     |                |      | `I2` | `N1` | `I1` |      |
| 5     |                |      |      | `I2` | `N1` | `I1` |
| 6     |                |      |      |      | `I2` | `N1` |
| 7     |                |      |      |      |      | `I2` |

Would have lost 2 cycles in this case without using forwarding (the dependent instruction is separated by 1 instruction, so 3 - 1 = 2)

| Cycle | Instruction in | F    | D    | X    | M    | W    |
| ----- | -------------- | ---- | ---- | ---- | ---- | ---- |
| 1     | `I1`           | `I1` |      |      |      |      |
| 2     | `N1`           | `N1` | `I1` |      |      |      |
| 3     | `N2`           | `N2` | `N1` | `I1` |      |      |
| 4     | `I2`           | `I2` | `N2` | `N1` | `I1` |      |
| 5     |                |      | `I2` | `N2` | `N1` | `I1` |
| 6     |                |      |      | `I2` | `N2` | `N1` |
| 7     |                |      |      |      | `I2` | `N2` |
| 8     |                |      |      |      |      | `I2` |

Still lost 0 cycles. Even though we have 2 dependent instructions.

### Back-to-Back Load-Use Hazard $I1{d\atop{\to}}I2$ with Forwarding

## Pipeline Performance

Suppose we are processing a long sequence of $n>>5$ instructions on the PIPE implementation.

Ignoring pipeline startup and draining cycles, how many cycles $c$ will this take?

Clearly, $c\geq n$. Let $c=n+b$ with $b\geq 0$. Then, **cycles per instruction (CPI)** is $=\frac{c}{n}=\frac{{n+b}}{n}=1+\frac{b}{n}$

The **penalty term** is $p=\frac{b}{n}$.

### Approximating the Penalty Term

Approximate the penalty term $p=\frac{b}{n}$ based on causes.

- Load penalty $lp$: 1 cycle for every (back-to-back) load use hazard ^07c485
- Misprediction penalty $mp$: 2 cycles for every mispredicted branch ^e4a29f
- Return penalty $rp$: 1 cycle for every `ret` instruction. ^ced3cf

$p\approx lp+mp+rp$

- Estimate the penalty terms based on the instruction frequencies and condition frequencies in the execution trace

CPI $=1+p\approx 1+lp+mp+rp$.
