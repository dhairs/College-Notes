## Introduction to Digital Design and Logic Gates

### Analog vs. Digital

The idea that we talk about 'digital circuits' must imply that there are other types of circuits. Those other types are *analog* circuits. 

- Analog pertains to continuous waveforms, and using those waves for the data
	- Analog design deals with continuous waveforms where the *exact* waveforms are essential for amplification, filtering, sensing, etc

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
- Logical low, or low voltage, or Vss, or 0, or "False",  or "De-asserted" all mean the same thing: Logical 0

#### Signals, timing, and delay through gates

In reality, we don't purely have a 0 or a 1, because signals must have rising and falling times. Recall [RC circuits](https://www.youtube.com/watch?v=PLQrPqYlPmI&pp=ygULcmMgY2lyY3VpdHM%3D) from AP Physics C E&M. This is a very similar concept.