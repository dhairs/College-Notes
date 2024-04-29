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

Speedup is $\frac{14.29}{3.12}=4.61$. Diminishing Returns.

### $k$ Uniform Pieces

Latency would be $k\cdot (\frac{300}{k}+20)\text{ ps} = (300 + 20k) \text{ ps}$ 

Throughput would be $\frac{1\text{ instruction}}{(\frac{300}{k}+20)\times10^{-12}s} = \frac{1000k}{300+20k} \text{ GIPS}$

As $k\to\infty: \text{latency}\to\infty, \text{throughput}\to 50\text{ GIPS}$

$\text{Speedup}\to \frac{50}{3.12}=16.02$ 


## Pipelining with Feedback

