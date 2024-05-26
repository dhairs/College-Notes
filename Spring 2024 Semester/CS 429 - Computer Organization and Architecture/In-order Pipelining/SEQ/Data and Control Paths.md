## Assembling the Data Path (F, D)

![[Data Path Block Diagrams]]

## Control Signals for D and X

- `src2_sel`: $op\in \{\text{STUR}\}$ 

- `valb_sel`: $op\in \{\text{ADDS, ANDS, SUBS, CMP, TST, ORR, EOR}\}$
- `set_cc`: $op\in \{\text{ADDS, ANDS, SUBS, CMP, TST}\}$

- `ALUop[3:0]`: ``

## Control Signals for M, W, and U

- `dmem_read`: $op\in \{\text{LDUR}\}$
- `dmem_write`: $op\in \{\text{STUR}\}$

- `dst_sel`: $op\in \{\text{BL}\}$
- `wval_sel`: $op\in \{\text{LDUR}\}$
- `w_enable`: $op\notin \{\text{STUR, B, B.cond, RET, NOP, HLT, CMP, TST}\}$

## Architectural Status Logic

STAT, in order of decreasing priority, is:
- `STAT_ADR`: if `dmem_err`
- `STAT_INS`: if (`imem_err` $\vee op \in \{\text{ERROR}\})$
- `STAT_HLT`: if $op\in\{\text{HLT}\}$
- `STAT_AOK` otherwise