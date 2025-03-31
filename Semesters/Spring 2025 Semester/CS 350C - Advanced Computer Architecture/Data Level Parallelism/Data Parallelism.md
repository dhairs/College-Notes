## Why?

While we already have instruction level parallelism, some loop iterations and other code can benefit from parallel computation. The most obvious example is graphics processing in GPUs. Often-times, these computations are (or can be thought of as) a vector that is multiplied by a scalar or other vector. 

## Necessary Architectural Resources

**Vector registers**: each holds a vector of maximum length $MVL$ (max vector length)

**Vector functional units**: Fully pipelined, II = 1 cycle

**Vector Load/Store Unit**: Fully pipelined

**Predicate registers**: to support conditional execution

**Optimization: Dynamic Register Configuration**: Allows flexible trading of between number of vectors, width of vector elements, and $MVL$.
- E.g. 1 [[Special Notation#Kibibyte (KiB)|KiB]] of vector register space, configure as 4 VRs of doubles, each VR gets 256 B, so $MVL=32$

Can disable VRs under program control, reducing program state that needs to be saved on context switches.

## Modeling Execution Time

We can model the execution time as a function of three factors:
- Length of operand vectors
- Data dependences
- Structural hazards (trying to put more data through than is possible)

Assume that in this example the Functional Unit processes one element per clock cycle.

We can handle read-after-write (RAW) dependences by **chaining**: essentially a pipelined version of forwarding that allows a dependent vector operation to start as soon as individual elements of its vector source operand become available.


We can group vector instructions into different **convoys**
- A **convoy** is a set of vector instructions that have no structural hazards and could therefore potentially execute together
- A **chime** is the unit of time to execute one convoy

The **model** is:
- Time for one chime $\propto$ vector length (proportional)
- Total time $\propto$ number of convoys
- For $m$ convoys and vectors of 

Assume the following code:

```asm
L1: V0 <- (X5) # Vector Load
L2: V1 <- V0 * F0 # Vector * Scalar
L3: V2 <- (X6) # Vector Load
L4: V3 <- V1 + V2 # Vector + Vector
L5: (X6) <- V3 # Vector Store
```

