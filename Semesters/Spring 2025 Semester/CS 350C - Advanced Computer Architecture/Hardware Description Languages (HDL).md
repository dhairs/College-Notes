## Definition


## Types
### VHSIC Hardware Description Language (VHDL)
- VHSIC means Very High Speed Integrated Circuit
- Originally developed under funding from the department of defense
- Originally meant for describe and document, not synthesize hardware

### [[Verilog]]
- Developed by the industry same time as VHDL
- Gateway Design Automation
- Syntactic roots in "C"

### Others
- System C: design extensions to C++
- System Verilog: an extension of Verilog including all of Verilog and object-oriented extensions for verification
## Behavioral vs. Structural

**Behavioral description**: specifies the design at algorithmic level without associating to any specific physical parts, components, or implementations.
- $C=A+B$

The behavioral description is often also called the register transfer level, or RTL.

**Structural description**: specific components or specific implementations of components are associated with the design.
- Adder implementation using AND-OR gates
- Adder using XOR gates