## What is System Verilog?

SystemVerilog is a successor/extension to [[Verilog]] that fixes a lot of common issues with syntax in the original language.

## Four-Valued Logic

Following the logic of a high-impedance floating wire, we need to have 4 possible values. Sometimes, we cannot tell when a device is floating in value. It could possibly have issues with pulling up or pulling down, which could leave an intermediary voltage value. As a result, we need to have this in our simulations.

In SystemVerilog, there are 4 values that can occur:
- 0: false
- 1: true
- z: floating
- x: invalid (don't know, don't care)

### Truth Table of Four-Valued Logic

| AND | 0   | 1   | z   | x   |
| --- | --- | --- | --- | --- |
| 0   | 0   | 0   | x   | x   |
| 1   | 0   | 1   | x   | x   |
| z   | x   | x   | x   | x   |
| x   | x   | x   | x   | x   |

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

### Logic Gates with Delays

```systemverilog
`timescale 1ns/1ps
module example(input logic a, b, c, output logic y);
	logic ab, bb, cb, n1, n2, n3;
	assign #1 {ab, bb, cb} = ~{a`, b, c};
endmodule
```

### Register

```systemverilog
module flop(input logic clk, input logic [3:0] d, output logic [3:0] q);
	always_ff @(posedge clk)
		q <= d;
endmodule
```

There is also a `negedge` word for the clock `clk`.
### Initial and Always

 **Initial**: only do this once at the start
 **Always**: do this every time	
 - Can be in form `always @(condition list)`
Three types of always:
- `always_ff` (flip flop)
- `always_latch` (level-sensitive latch)
- `always_comb` (combinational)

### Resettable Register (Asynchronous)

```systemverilog
module flopr_async(input logic clk, reset, input logic [3:0] d, output logic [3:0] q);
	always_ff @(posedge clk, posedge reset)
	if (reset) q <= 'b0;
	else q <= d;
endmodule
```

### Resettable Register (Synchronous)

```systemverilog
module flopr_sync(input logic clk, reset, input logic [3:0] d, output logic [3:0] q);
	always_ff @(posedge clk)
	if (reset) q <= 'b0;
	else q <= d;
endmodule
```

### Resettable Enabled Register (Synchronous)

```systemverilog
module flopr_sync(input logic clk, reset, en, input logic [3:0] d, output logic [3:0] q);
	always_ff @(posedge clk)
	if (reset) q <= 'b0;
	else if (en) q <= d;
endmodule
```

### Synchronizer

```systemverilog
module sync(input logic clk, d, output logic q);
	logic n1;
	
	always_ff @(posedge clk)
	begin
		n1 <= d;
		q <= n1;
	end
endmodule
```

### Level Sensitive D Latch

```systemverilog
module latch(input logic clk, d, output logic q);
	always_latch @(clk,d)
	if (clk) q <= d
endmodule
```

### Inverter Using `always`

```systemverilog
module inv(input logic [3:0] a, output logic [3:0] y);
	always_comb @(*) // anything happens
		y = ~a;
endmodule
```

### Assignment Statements

If doing an assignment outside of an `always` block:
- continuous assignment using the `assign` keyword
- evaluated *concurrently*

Inside an `always` block:
- block assignment using `=` (use this for combinational logic)
- non-blocking assignment using `<=` (use for sequential logic)

### Full Adder using `always`

```systemverilog
module fulladder(input logic a, b, cin, output logic s, cout);
	logic p, g;
	
	always_comb
		begin
			p = a ^ b;
			g  = a & b;
			s = p ^ cin;
			cout = g | (p & cin);
		end
endmodule
```

### Seven-Segment Display Decoder

```systemverilog
module sevenseg(input logic[3:0] data, output logic [6:0] segments);
	always_comb
		case(data)
			0: segments = 7'b111_1110;
			1: segments = 7'b011_0000;
			...
			9: segments = ...;
			default: segments = ...;
		endcase
endmodule
```

### Priority Circuit

#### With Don't Cares

```systemverilog
module priority_casez(input logic[3:0] a, output logic[3:0] y);
	always_comb
		casez(a) 
			4'b1???: y = 4'b1000; // don't care about the rest of this #
		endcase
endmodule
```

### Multiplier

#### Unsigned

#### Signed

### Parameterized N: $2^N$ Decoder

```systemverilog
module decoder
	#(parameter N=3)
	(input logic[N=1:0] a, output logic[2**N-1:0] y);
	
	always_comb
		begin
			y = 0;
			y[a] = 1;
		end
endmodule
```

### Generate Statement

Be careful when using this.

```systemverilog
module andN
	#(parameter width=8)
	(input logic[width-1:0] a, output logic y);
	genvar i;
	logic[width-1] x;
	
	generate
		assign x[0] = a[0];
		for(i = 1; i < width; i = i + 1) begin: forloop
			 assign x[i] = a[i] & x[i-1];
		end
	endgenerate
	
	assign y = x[width-1];
endmodule
```

When we need to define structure in variable sized modules/subsystems, we have to use `generate` to define the structure in a very metaprogramming-esque way.

### Making a Test Bench

#### Basic Test Bench

```systemverilog
module testbench2();
	logic a, b, c, y;
	// instantiate device under test
	sillyfunction dut(a, b, c, y);
	initial begin
		a = 0; b= 0; c = 0; #10;
		assert(y === 1) else $error ("000 failed.");
		c = 1;
		assert (y === 0) else $error ("001 failed.");
		...
	end
endmodule
```

#### File Driven Test Bench

It can be better to create a system with a behavioral implementation.

```systemverilog
module testbench3();
	logic a, b, c, y;
	logic[31:0] vectornum, errors;
	logic[3:0] testv[10000:0];
	// instantiate device under test
	sillyfunction dut(a, b, c, y);
	always begin
		clk = 1; $5; clk = 0; #5;
	end
	
	initial begin
		$readmemb("example.tv", testv); // read binray file into memory
		vectornum = 0; errors = 0;
		reset = 1; #27; reset = 0;
	end
	
	always @(posedge clk) begin
		#1; {a, b, c, exp} = testv[vectornum];
	end

	always @(negedge clk) begin
		if(~reset) begin
			if(y !== exp) begin
				$display("Error: inputs = %b ", {a, b, c});
				$display("Output = %b (expected %b)", y, exp);
				errors++;
			end
			vectornum++; ...
		end
endmodule

```