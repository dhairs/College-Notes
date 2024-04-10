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
- *from* instruction $i$: from the end of the combinational logic block in the X stage, equivalent to `M_in`, or from `M_out`, or from `W->in`, or from `W->out`
- *to* intercept instruction $j$: at the end of the combinational logic block in the D stage, just after incorrect values have been read for the registers
- *so* that the correct bits are presented at the *clock's edge* to be latched into the X pipeline register, ready for the next cycle
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