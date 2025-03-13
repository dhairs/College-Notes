## Memory Wall Problem

Optimization focus so far has been reducing the [[Scalar Optimizations|amount of computation]]. However, on modern machine, most programs that access a lot of data are memory bound. The latency of [[Main Memory#DRAM|DRAM]] is usually on the order of 100-1000 cycles.

Caches can reduce the effective latency of memory access, but programs may need to be rewritten to take full advantage of caches. 