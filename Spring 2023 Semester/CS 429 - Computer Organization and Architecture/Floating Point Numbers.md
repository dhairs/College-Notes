## The Design Problem

With 64-bit integers, we only get `18,446,744,073,709,600,000` distinct values. But quantities in physics and mathematics can easily go well beyond this.

We need to find something that is not only efficient in storage space, but also in computational time, because we only have so many resources.

![[Drawing 2024-02-05 14.11.05.excalidraw]]

## Choice 1: Fixed Point

Represent a number $x$ as $\pm x_i * x_f$ where:
- $x_i$ is the integer part of $x$, represented using $a$ radix-$k$ digits
- 