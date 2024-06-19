# Bits and Bit Technologies

## What is a Bit?
**BIT** - **BI**nary digi**T**

A bit is an 'entity' having *two* distinct, *distinguishable*, *discrete* states. Generically designated as $\circ$ and $|$.

A bit can be realized by any physical object that has two stable states that can be distinguished confidently.  
- Think of a transistor's on and off state — when passing current, the bit is $|$, when no current, the bit is $\circ$
- Additionally, think of a CAN bus, there is no off or on state, but rather a low and high voltage to differentiate. One line runs usually at 2.5v and the other usually around 5v, differences between both wires can be interpreted as $|$ or $\circ$ because they are predictable and stable.

## Semiconductors

Start with silicon, 

- **MOSFET** - **M**etal-**O**xide-**S**emiconductor **F**ield-**E**ffect **T**ransistor ^e5350b
	- controls the *current* between the source and the drain using the electric field generated b the gate *voltage* as the control variable
	- we use the cut-off region ($\circ$) and saturation region ($|$) digitally
	- we don't use the linear region because it's not stable, leads to distortion, and can lead to incorrect bits.

## Ferromagnetism

- Work by magnetizing a thin film of ferromagnetic material on both sides of a disk
- Sequential changes in the direction of magnetization (at a granularity of millions of magnetic domains, forming a magnetic dipole and generating a magnetic field) represent bits

## Byte

One **Byte (B)** is defined as an aggregation of **8 bits**.

## Nibble

One **Nibble** is defined as an aggregation of **4 bits**, or $\frac{1}{2}$ of a [](Bits%20and%20Bit%20Technologies.md#Byte|Byte).
