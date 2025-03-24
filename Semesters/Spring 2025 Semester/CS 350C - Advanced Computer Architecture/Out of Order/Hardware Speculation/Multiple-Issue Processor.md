## Renaming for a Multiple-Issue Processor

Consider a processor with a fetch width of 4, with 8 inputs and 4 results. Each input needs to be read from a physical register. We want to map each output from architectural to physical registers. Dependences must be handled.

Assume 16 architectural registers and 128 physical (µarch) registers. Architectural registers only exist as a concept. At any instant of time, an architectural register is mapped to a physical register.

The initial mapping is $\mu_{0}=\{ r_{i}\to p_{i}\}^{15}_{i=0}$. This mapping evolves with each instruction.

If instruction $i$ is $r_{d}=\text{op}(r_{m},r_{n})$, then:
- $\mu_{i+1}=\mu_{i}\oplus r_{d}\to p_{j}$ where $p_{j}$ is a new physical register.

```asm
mov r1, 1
add r1, r2, r3
add r4, r1, 1
```

can become 

```asm
mov pl1, 1
add pl2, p2, p3
add p41, p12, 1
```

This works for a single fetch width, but not with our wanted one of 4, because the process needs to be able to rename 4 in a single cycle, while keeping track of dependences. We also don't want to serialize because that defeats the entire point of doing this.

## Mechanisms

We need three key blocks to be able to perform multi-width renaming:
- Register Alias Table
- Dependence Check Logic
- Free Register List

Consider this code:

```asm
// µ0
add r3, r1, r2
add r5, r3, r4
add r8, r6, r7
add r9, r8, r8
```

should become

```asm
// µ4
add p23, p1, p2
add p25, p23, p4
add p18, p6, p7
add p39, p18, p18
```

In a single cycle, we want to transition from $\mu_{0}$ to $\mu_{4}$ while renaming each instruction $i$ correctly from the mapping $u_{i-1}$.

### Register Alias Table (RAT) (AKA Register Rename Table)

Translate architectural register ID to physical register ID

### Dependence Check Logic (DCL)

Take care of dependences between instructions renamed in the same cycle.

### Free Register List (FRL)

Maintain a list of unmapped physical registers.