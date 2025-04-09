
Google's DNN ASIC. Specifically meant to be amazing at dense matrix-matrix multiplication. 256x256 8-bit unit. 

Large software-managed data buffer (scratchpad).

Coprocessor on the PCIe bus.

If you don't have the ability to do computation with a cache in parallel, you use a **systolic** algorithm. A massively parallel pipeline/array of stuff with a regular connectivity pattern/clock cycle. Compute, push, communicate, synchronized.

## Systolic Operation of TPU


## TPU Guidelines

Use dedicated memories: 24 MiB dedicated buffer, 4 MiB accumulator buffers

Invest resources in arithmetic units and dedicated memories: 60% of the memory and 250x the arithmetic units of a server-class CPU

Use the easiest form of parallelism that matches the domain: exploits 2D SIMD parallelism

Reduce the data size