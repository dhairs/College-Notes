## What is it

When optimizing programs, we need to know the way data is passed through functions and different branches. This is important in making sure that the optimized program is the equivalent to the original program.

## Inference Rules Extended

This extends the first, follow, and nullable sets we learned [[Inference Rules|earlier]].

### Follow
$\$\in \text{FOLLOW}(S)$

$\text{FOLLOW}(S)=\text{FOLLOW}(S)\cup\{\$\}$

The follow set is the [[Power Set|power set]] of $T$ terminals, and thus has $2^T$ elements.

## Using Fixpoint Theorem for Dataflow Analysis

We want to be able to expose opportunities for optimization that are safe to be done. We, for this reason, need to keep track of the flow of expressions through the program. This all follows the lattice theory and set theorems we talked about in being able to [[Solving Fixpoint Equations|solve fixpoint equations]].

This is within a single procedure, though it is possible to do inter-procedural dataflow analysis.

We can do a topological sort if we have a directed acyclic graph (DAG), but this assumption goes away as soon as we have loops and therefore no longer have an acyclic graph. For these situations, it is important to start using the fixpoint methods to optimize. 

### Dataflow Equations

System of fixpoint equations in which unknowns are solutions to the dataflow problem at different points in program.

Solve the system of equations as described in previous lecture.

For many problems, this gives the meet-over-paths solution, and for other problems, it gives a "safe" approximation to the MOP solution.

We'll solve it using fixpoint equations.

```mermaid
graph TD
    A[START] --> B[d1<br>a:= ....]
    B --> C{if pa}
    C -- true --> D[d2<br>a:= ....]
    C -- false --> E[d3<br>a:= ....]
    D --> F[...a...]
    E --> F
    F --> G[" "]
```

### Reaching Definitions: Multiple Variables

You can solve for one variable at a time, but its better to solve for all of them at once.

```mermaid
graph TD
    A[START] --> B{if #40;c#41;}
    B -- true --> C[x = y + 1]
    B -- false --> I[z = x]
    C --> D[y = 2*z]
    D --> E{if #40;d#41;}
    E -- true --> F[x = y + z]
    E -- false --> G[z = 1]
    F --> G
    G --> B
    I --> J["DONE"]

    linkStyle 0,1,2,3,4,5,6,7,8 stroke-width:2px;  

    classDef highlight fill:#ccf,stroke:#888,stroke-width:2px
    class A,B,C,D,E,F,G,H,I,J highlight
```

### Observations of the Fixpoint Approach

System of equations can be solved to find the least solution. The iterative method for solving equations will converge even though there are an unbounded number of paths in the program. 

## Classifications of Dataflow Problems

**Direction of Information Propagation**:
- **Forward-flow**: information propagates in the direction of control-flow from the input to output
- **Backward-flow**: information propagates in the reverse direction of control-flow from the output to input

**All-paths vs. any-path**:
- **All-paths problem**: dataflow fact is true at some point in the program if it is true along **all** paths to/from that point
- **Any-path problem**: dataflow fact is true at some point in the program if it is true along **any** path to/from that point


> [!FAQ] How can reaching definitions be classified?
> They are classified as **forward-flow**, **any-path** because you follow the control flow graph, and any way to reach a node includes the dataflow fact.


