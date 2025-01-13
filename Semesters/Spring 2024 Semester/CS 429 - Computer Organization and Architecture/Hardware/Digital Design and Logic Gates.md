## Introduction to Digital Design and Logic Gates

### Analog vs. Digital

The idea that we talk about 'digital circuits' must imply that there are other types of circuits. Those other types are _analog_ circuits.

- Analog pertains to continuous waveforms, and using those waves for the data

  - Analog design deals with continuous waveforms where the _exact_ waveforms are essential for amplification, filtering, sensing, etc

- Digital pertains to discrete states for data
  - Digital design deals with transistors and logic gates as fundamental building blocks where the information is represented in only two states: [[Bits and Bit Technologies#What is a Bit?|on and off]]

### Boolean Algebra

This is a branch of algebra where variables take only one of two values: True (1) or False (0). The same as a bit.

We are therefore able to use operators like AND (.), OR (+), NOT (! or '), etc. You can find all of these in [[Logical operators]]. We can do expressions the same we do in discrete math.

Boolean Expressions are combinations of variables using the above operators:

- Ex: A.B + B.C + C'.D
  - This means (A AND B) OR (B AND C) OR (NOT C AND D)

### Power & Ground and Logic Levels

Along with logical signals, power and ground is of course required for our digital circuits.

- Logical high, or high voltage, or Vdd, or Vcc, or 1, or "True", or "Asserted" all mean the same thing: Logical 1
- Logical low, or low voltage, or Vss, or 0, or "False", or "De-asserted" all mean the same thing: Logical 0

#### Signals, timing, and delay through gates

In reality, we don't purely have a 0 or a 1, because signals must have rising and falling times. The potential of the system or gate takes time to reach state. So, we only use the logical state in Computer Science.

Additionally, logic gates have to react to their inputs, and therefore their output has a delay. This is called **gate delay** or **[propagation delay](https://en.wikipedia.org/wiki/Signal_propagation_delay#:~:text=Logic gates can have propagation,on the technology being used.)**. Similar to a person reacting to their inputs (perception), electronic circuits still have to react, though at a much smaller scale and on a much quicker timeframe. For this reason, logic gates traditionally have delays ranging from more than 10 nanoseconds all the way down to the picosecond range.

Wires also conduct electricity, but they also have delays. This is completely because of Resistivity and Capacitance of wires, and in addition, the possibility of noise or deformation to the signal. Recall [RC circuits](https://www.youtube.com/watch?v=PLQrPqYlPmI&pp=ygULcmMgY2lyY3VpdHM%3D) from [AP Physics C E&M](https://www.youtube.com/watch?v=FYsfp4bZc2w&t=631s&pp=ygULcmMgY2lyY3VpdHM%3D). This is very similar, if not the exact reason, behind wire delays.

### Digital Logic and Circuits

A digital logic circuit is designed using logic gates connected by signal wires that implement a boolean function.

### Sum of Products (SOP)

Mathematically, a minterm is any product of $n$ literals where each of the $n$ variable appears once in the product. A boolean function or expression is in Disjunctive Normal Form.

### Universal Gates

NAND and NOR are Universal gates, because given _any_ boolean expression, you can convert them into an expression of all NANDs or all NORs, using [[Basic Equivalences|DeMorgan's Laws]].

## Combinational Logic and the Arithmetic Logic Unit

### Combinational Logic/Circuits

A combinational circuit's output is dependent on the current value of the inputs, without any regard to the past values or results.

So far, we've talked about combinational logic gates, they are the building blocks for combinational circuits, described by Boolean Expressions.

### Half and Full Adders

Half Adders (HA) and Full Adders (FA) are good examples of combinational logic. Recall the idea of an [[Integer Arithmetic#$n$-bit Adder|n-bit adder]].

HA's sum is = a'.b +a.b

HA's carry out = a.b

FA's sum = a'.b'.c + a'.b.c' + a.b'.c' + a.b.c

FA's carry out = a.b + b.c + c.a

If the inputs change at any point in time, the outputs will as well.

### The charm-v2 ALU

### Condition Flags

Definitions:

- $N {\text{def}\atop{=}} val_ex[63]$
