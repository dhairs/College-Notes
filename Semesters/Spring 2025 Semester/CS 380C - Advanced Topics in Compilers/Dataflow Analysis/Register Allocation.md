## Code Generation Strategies

Simple method: generate stack code
- All variables and user-defined temporaries are allocated on stack
- use registers as temporaries when evaluating expressions
	- x86: and to return values from function calls

The better strategy is to use registers because they are faster and part of the execution cycle itself.
- Local variables and user-defined temporaries can be allocated to registers if you have enough

This also means we can use registers to return values from function calls to perform some instructions.

The approach is to generate "abstract" assembly code in which you assume you have an unbounded number of registers and perform register allocation.

We want to assign **temporary variables** to some fixed set of registers. To do this, we **first** need to know which variables are live after each instruction.
- two simultaneously live variables cannot be put into the same register
	- This makes sense because you might have to access them both in one cycle.

In addition, we also want to make sure that we save and restore register state, so we want to **limit register usage**.

## Method

For every node $n$ in a [[Control Flow Graphs|CFG]], we have $\text{out}[n]$
- this is the set of temporaries that are [[Dataflow Analysis#Live Variables|live]] out of $n$

Two variables **interfere** if:
- both are initially live
- both appear in $\text{out}[n]$ for any $n$


> [!faq] How to allocate register to variables?
> We use interference graphs and graph coloring theory.

## Interference Graphs

This follows graph coloring theory. 

The **nodes** of the graph are **variables** and the **edges** are **variables** that interfere with one another. Nodes will be assigned a **color** corresponding to the register assigned to the variable. Two colors can't be next to another in the graph.


| ![[interference graph register allocation.png]]                                   |
| --------------------------------------------------------------------------------- |
| https://www.cs.utexas.edu/~pingali/CS380C/2025/lectures/Register%20Allocation.pdf |

### Graph Coloring

There are a few questions that come up regarding graph coloring:
- Can we efficiently find a coloring of the graph whenever possible?
- Can we efficiently find an optimal coloring of the graph?
- How do we choose registers to avoid move instructions?
- What do we do when there aren't enough colors (registers) to color the graph?

### Kempe's Heuristic

Kempe's algorithm for finding a $K$-coloring of a graph.

#### Step 1 (Simplify):

Find a node with **at most** $K-1$ edges and cut it out of the graph. We remember this node on a stack for later stages

The intuition behind this step is that once a coloring is found for the simpler graph, we can always color the node we saved on the stack.

#### Step 2 (Color):

When the simplified graph has been colored, add back the node on the top of the stack and assign it a color not taken by one of the adjacent nodes.


/h