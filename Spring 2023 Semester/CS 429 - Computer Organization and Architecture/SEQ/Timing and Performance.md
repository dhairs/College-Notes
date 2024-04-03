## In a Sequential Stage System

Suppose propagation delays are:
- 300 picoseconds (ps) for the combinational logic
- 20 ps for the register

The **latency** is the time between the start and end of execution of an instruction

In this case: (300 + 20) ps = 320 ps

Minimum clock cycle time: 320 ps
- Maximum clock frequency = $\frac{1}{320\times10^{-12}} \text{Hz} = 3.12\text{GHz}$

The **throughput** is the number of instructions executed per unit of time in **steady state**
- $\frac{1\text{ instruction}}{320\times10^{-12}s}=3.12\times10^9\text{ IPS}=3.12\text{ GIPS}$ (IPS is instructions per second)

We can do better than this is (how?)
- We have two metrics for performance: latency and throughput
- We physically can't decrease the latency of a system without changing it. So what can we do? **Increase throughput**

Though it feels counterintuitive, we need to have a way to increase throughput. Right now, when an instruction moves through the stages of processing, we have the issue of previous stages being idle. Essentially, we're wasting time.

Enter pipelining

## Pipelining

Suppose the propagation delays are the same as before, 300 ps for combinational logic, 20 ps for the register
- But now, lets break up the combinational logic into 3 pieces, each with 100 pc of propagation delay (**uniform partitioning**)

Then, we could overlap (**pipeline**) the execution of 3 successive instructions by adding registers after each piece A, B, and C.

The latency is now $3\times(100+20)\text{ ps} = 360\text{ ps}$ 

Minimum clock cycle time is now $(100 + 20)\text{ ps} = 120\text{ ps}$ 

### Non-Uniform Partitioning

If the partitioning is non-uniform, then the gain from pipelining is limited by the speed of the slowest stage (the bottleneck)

The latency is now $3\times(\text{max}(50,150,100)+20)\text{ ps} = 510 \text{ ps}$ 

The minimum clock cycle is now 170 ps

### Diminishing Returns of Deep Pipelining

Suppose we partition the logic into 6 pieces, each of 50 ps latency

The latency is now $6\times(50+20)\text{ ps} = 420 \text{ ps}$

Minimum clock cycle time is now $(50 + 20) \text{ ps} = 70\text{ ps}$
- Max clock frequency is $14.29\text{ GHz}$ 

Throughput is 14.29 GIPS

Speedup is $\frac{14.29}{3.12}=4.61$. Diminshing Returns

### $k$ Uniform Pieces

Latency would be $k\cdot (\frac{300}{k}+20)\text{ ps} = (300 + 20k) \text{ ps}$ 

Throughput would be $\frac{1\text{ instructi}}