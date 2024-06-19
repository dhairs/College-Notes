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

Enter [pipelining](Intro%20to%20Pipelining.md).