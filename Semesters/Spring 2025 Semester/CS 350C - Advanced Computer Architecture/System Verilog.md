## What is System Verilog?

SystemVerilog is a successor/extension to [[Verilog]] that fixes a lot of common issues with syntax in the original language.

## Four-Valued Logic

In SystemVerilog, there are 4 values that can occur:
``

## Syntax

Will pick up on the syntax directly from where we left off on [[Verilog#Syntax|Verilog]]. 

### Inverters

```systemverilog
module inv(input logic [3:0] a, output logic [3:0] y);
	assign y = ~a; // flips individual bits of the BUS a
endmodule
```

### Logic Gates

```systemverilog
module gates(input logic[3:0] a, b, output logic [3:0] y1, y2, y3, y4, y5);
	assign y1 = a & b; // a AND b
	assign y2 = a | b; // a OR b
	assign y3 = a ^ b; // a XOR b
	assign y4 = ~(a & b); // NOT (a AND b)
	assign y5 ~(a | b); // NOT (a OR b)
endmodule
```

### Multi-Bit AND

Instead of manually writing out all bits of BUS a, you can just apply the scalar AND to all of the bits of the input until we have a single result.

```systemverilog
module gates(input logic [7:0] a, output logic y);
	assign y = &a;
endmodule
```

### 2:1 Multiplexer

Just a C-like ternary operator.

```systemverilog
module mux2(input logic[3:0] d0, d1, input logic s, output logic [3:0] y);
	assign y = s ? d1 : d0;
endmodule
```

### 4:1 Multiplexer (Behavioral)

We now need to add bits to s to choose. This is behavioral (not structural) because we define *what* the behavior is, not *how* to implement it.

```systemverilog
module mux2(input logic[3:0] d0, d1, d2, d3, input logic[1:0] s, output logic [3:0] y);
	assign y = s[1] ? (s[0] ? d3 : d2) : (s[0] ? d1 : d0);
endmodule
```

### 4:1 Multiplexer (Structural)

Need to use 2:1 multiplexer as a base for making this.

```systemverilog
module mux2(input logic[3:0] d0, d1, d2, d3, input logic[1:0] s, output logic [3:0] y);
	logic [3:0] low, high;
	mux2 lowmux(d0, d1, s[0], low);
	mux2 highmux(d1, d3, s[0], high);
	mux2 finalmux(low, high, s[1], y);
endmodule
```

### Full Adder

```systemverilog
module fulladder(input logic a, b, cin, output logic s, cout);
	logic p, g;
	assign p = a ^ b;
	assign s =  ^ cin;
	assign cout = g | (p & cin);
endmodule
```

### Tristate Buffer

```systemverilog
module tristate (input logic [3:0] a, input logic en, output logic [3:0] y);
	assign y = en ? A : 4'bz;
endmodule
```