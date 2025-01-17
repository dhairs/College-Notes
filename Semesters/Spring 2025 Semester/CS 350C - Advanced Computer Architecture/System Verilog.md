## What is System Verilog?

SystemVerilog is a successor/extension to [[Verilog]] that fixes a lot of common issues with syntax in the original language.

## Syntax

Will pick up on the syntax directly from where we left off on [[Verilog#Syntax|Verilog]]. 

### Inverters

```systemverilog
module inv(input logic [3:0] a, output logic [3:0] y);
	assign y = ~a;
endmodule
```

### Logic Gates

```systemverilog
module gates(input logic[3:0] a, b, output logic [3:0] y1, y2, y3, y4, y5);

	assign y1 = a & b;
	assign y2 = a | b;
	assign y3 = a ^ b;
	assign y4 = ~(a & b);
	assign y5 ~(a | b)
```