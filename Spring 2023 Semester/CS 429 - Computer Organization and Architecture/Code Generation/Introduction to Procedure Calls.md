# Procedure Calls

Recall how code is generated for very simple constructs in code: [[Introduction to Code Generation]].

We need to understand how procedures are called in the underlying system, and how we can encode them in assembly.

## What is a Procedure?

A means of encapsulating both code *and* data, resulting in both **abstraction** and **composition**.

A function in JavaScript or C is a procedure. It's not the same as a class, where state can be stored across method calls and between methods.

## What is "`P` calls `Q`"?

There are three mechanisms that are in effect together when we want `P` calls `Q`:
1. **Control Transfer**: Our transfer must be bidirectional. We must pass control from `P` to `Q` and then *return* control from `Q` back to `P`
	1. This makes sense in the context of calling a function from another function. We can call a function to do something and then continue in the original function (`P`)'s control flow
2. **Data Transfer**: Passing parameters from `P` to `Q`, and returning *results* from `Q` back to `P`
	1. This makes sense, think of return statements and using the data from one method in another in C. Like using a method for an API request, the parameters are the endpoints, and the results are the server response
3. **State Management**: Isolating local states of `P` and `Q` from each other.
	1. Think of this in the context of recursion. We call the same function yet the state in both methods is different.

### Example Stack Call Control Flow

![[Procedure Control Flow Example]]

### Takeaways

- A procedure is different from a **procedure activation**
	- A procedure is **the** static (compile time) representation of the encapsulated functionality, capturing all possible execution paths for different input parameter values
		- There is **only one** of these in the code
	- A procedure activation is **a** dynamic (run-time) instance representing a procedure invoked with a specific set of input parameter values
		- Different procedure activations may take dramatically different paths through the same static code body.
- The behavior of "`P` calls `Q`" is fundamentally different from that of "`P` branches to the beginning of `Q`"
	- The difference is that "`P` calls `Q`" requires that control be returned to `P`, whereas in "`P` branches to the beginning of `Q`" there is no return address associated with the call
	- In "`P` calls `Q`", both have asymmetrical roles in the control flow
- The return address is *not unique* and is in general unknown for a procedure at compile time
	- There may be multiple call sites within a single caller (a function calls the same function from different parts of its code)
	- There may be multiple distinct callers (e.g., P and Q for R)
	- The calling procedure `P` and the called procedure `Q` may be compiled separately and brought together only at link time. As an extreme case, the caller may not even have been written when the callee was compiled.
- Calls and returns occur in matching pairs
	- A function call $P\to Q$ occurs, and then the return $Q\to P$ must also occur
	- Nested calls behave in a LIFO manner (i.e., the last procedure called is the first to return)
	- A **run-time stack** would be perfect for supporting nested calls
		- This is your program stack!!! We push new function calls *onto* the stack.
	- Different languages can have different organizations for procedure activation: static, stack-based (most common), and heap-based allocations are all possible

## AArch64

- The runtime stack grows from larger memory addressed down to smaller memory addresses.
- The stack "grows downwards"
- The `SP` (stack pointer) register points to the top of the stack.
- The `SUB` and `ADD` instructions are used to "open up" and "close down" arbitrary amounts of space on the stack.
	- This is known as the **activation record** or **stack frame**
	- Ex: when we request a function call that will take 80 bytes of data, we can simply do a subtraction from the stack pointer `SP` and 80 bytes.

- In this architecture, the stack grows downward, and the heap grows upward. Both of them can be interchanged, but they both have to close in on each other. This helps with flexibility between programs. When closing in on each other, we can have a huge stack and tiny heap, or the other way around. 
- Both **cannot** meet in the middle, we need a buffer zone.