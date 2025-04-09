
Google's DNN ASIC. Specifically meant to be amazing at dense matrix-matrix multiplication. 256x256 8-bit unit. 

Large software-managed data buffer (scratchpad).

Coprocessor on the PCIe bus.

If you don't have the ability to do computation with a cache in parallel, you use a **systolic** algorithm. A massively parallel pipeline/array of stuff with a regular connectivity pattern/clock cycle. Compute, push, communicate, synchronized.

## Systolic Operation of TPU

