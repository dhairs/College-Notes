## Syntax

- Generally case-sensitive
- All statements end with semicolon

### Identifiers
- Can include letters, numbers, underscore, and dollar sign
- Must begin with a letter or underscore

Verilog is a **concurrent language**.

**Concurrent statements**: statements always ready to execute. Get evaluated any time and every time a signal on the right side of the statement changes. 

Note that because of this, statements can usually be placed in any order.

### General Assignment Form

```verilog
assign #[delay] signal_name = expression;
```

### Example

```verilog
assign #5 C = A && B;
assign #5 E = C || D;
```

This assigns a propagation delay of 5ns to both gates and creates an AND gate called C from A and B going into an OR gate of C and D.

### Multiple bit signals 

```verilog
wire [3:0] B;
assign B = 4'b1100; // Assigns 1 to B[3], 1 to B[2], 0 to B[1], 0 to B[0]
```

## Modules
Basically a way of abstracting out smaller components/blocks. Helps create structure with the language.

$\text{Input}\rightarrow \text{Module}\rightarrow \text{Output}$.

### Syntax for Modules
```verilog
module [module_name] (module interface list);
[list-of-interface-ports]

[port-declarations]


```

#### Example
```verilog
module two_gates (A, B, D, E);
output E;
input A, B, D;

wire C;

assign C = A && B;
assign E = C || D;

endmodule
```

## Example of 1-bit Full Adder

```verilog
module FullAdder(X, Y, Cin, Cout, Sum);
output Cout, Sum;
input X, Y, Cin;


```

## Example of 4-bit Adder using 1-bit Full Adder

```verilog
module Adder4(S, Co, A, B, Ci);
output [3:0] S;
output Co;
input [3:0] A, B;
input Ci;

FullAdder FA0(A[0], B[0], Ci, C[1], S[0]);
FullAdder FA1(A[1], B[1], Ci, C[1], S[0]);
FullAdder FA2(A[2], B[2], Ci, C[1], S[0]);
FullAdder FA3(A[3], B[3], Ci, C[1], S[0]);
```