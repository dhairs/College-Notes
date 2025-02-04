## Optimizations

Code transformations must be done to improve the program, mainly to decrease execution time, but may also be used to decrease program size.

Optimizations **must** be safe. The resultant code must yield the same results as the original code, for **all possible executions**.

### Optimization Safety

Dead code elimination is a straightforward example. You can take code that isn't used at all, and remove it.

#### Example

```c
x = y + 1;
y = 2 * z;
if(d) x = y + z;
z = 1;
z = x;
```

Only the line `z = 1` is dead code in this example. 

This shows that control flow is necessary to be able to understand dead code.

#### Example With Loop

```c
while(exp) {
	x = y + 1;
	y = 2 * z;
	if(d) x = y + z;
	z = 1;
}
z = x;
```

In this case, nothing is dead code. Because `z = 1` can be used in the assignment to `y` in the second iteration of the while loop. This is a dependence and thus we have no definition free paths. 

#### Low-Level Code

It is much easier to build control flow and recognize dead code with low level code, because it is inherently linear.

## Control Flow Graphs

This is a graph representation of computation and control flow in the program. We use this as a framework for static analysis of the program control-flow.

Nodes are basic blocks: straight-line, single-entry code, no branching except at the end of the sequence.

The edges represent the possible flow of control from the end of one block to the beginning of another.