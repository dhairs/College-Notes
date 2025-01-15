## Syntax

- Generally case-sensitive
- All statements end with semicolon

### Identifiers
- Can include letters, numbers, underscore, and dollar sign
- Must begin with a letter or underscore

### Example

```verilog
assign #5 C = A && B;
assign #5 E = C || D;
```

This assigns a propagation delay of 5ns to both gates and creates an AND gate called C from A and B going into an OR gate of C and D.