## Definition of `switch`

The syntax of `switch` statements is: `switch (<expression>) <statement>`

A switch statement causes control to jump to, into, or past the statement that is the switch body


## Strategies for Generating `switch` statement code

### Case values are distributed sparsely over a wide range (Linear Search)
1. Generate code that uses a series of `if-else` statements at runtime to select the case label
2. Worst case selection time is **linear** in # of case labels - O(n)

### Case values are distributed densely over a wide range (Binary Search)
1. Generate code that uses binary search at runtime to select the case label
2. Worst case selection time is **logarithmic** in # of case labels - O(log n)

### Case values are in a narrow range (Jump Table)
1. Generate code that uses a **jump table** at runtime to select the case label
2. Selection time is **constant** - O(1)

To force `gcc` to generate jump tables, you can use `--param case-values-threshold=1`

#### What is a Jump Table?

A jump table is an array of pointers to code locations (i.e., an array of labels)
- This is a **machine-level abstraction**, a read-only data array whose elements are either addresses of machine instructions or data from which such addresses can be computed
	- So basically, we either store the pointer itself, or we store a delta (difference) between the current address and address of the next instruction that we want to jump to (see the black below)
- Not in the `C` standard, but available as a non-standard extension in `GNU C`

![Jump Tables](Jump%20Tables.svg)

