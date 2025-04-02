## NVIDIA CUDA

CUDA: *Computer Unified Device Architecture*

It is an extension of C++ and allows the user to write code for GPUs. Allows full C++ for the CPU (`host`) and a subset for the GPU (`device`). The GPU component is compiled into PTX, which defines a virtual machine and ISA for general-purpose parallel thread execution. It uses an infinite number of registers. PTX programs are translated at install time to the target hardware instruction set by the device driver (JIT compilation).

The CUDA command `nvcc` is a compiler driver that orchestrates the workflow. It produces a fat binary that contains both GPU and CPU code.

## Programming Model

### Kernel

A kernel is a C++ function that, when called, is executed $N$ times in parallel by $N$ different CUDA threads, as opposed to only once like regular C++ functions.

A kernel can be defined using the `__global__` declaration specifier.

The number of CUDA threads executing the context is specified using a new `<<<...>>>` execution configuration.

```cpp
// Kernel Def
__global__
void VecAdd(float *A, float *B, float *C) {
	int i = threadIdx.x;
	C[i] = A[i] + B[i];
}

int main() {
	...
	// Kernel Invocation with N Threads
	VecAdd<<<1, N>>> (A, B, C);
	...
}
```

Each thread that executes `VecAdd()` performs one addition.

### Thread Hierarchy

For convenience, `threadIdx` is a 3-component vector so that threads can be identified using a one-dimensional, two-dimensional, or three-dimensional *thread index*, forming a one-dimensional, two-dimensional, or three-dimensional block of threads called a **thread block**.
- All threads of a block are expected to reside on the same streaming multiprocessor (SM) core and must share the limited memory resources of that core. All threads of a block are guaranteed to be co-scheduled on a SM core. The current limit is 1024 threads per thread block.
- Thread blocks are independent by construction, threads within a block can cooperate via shared memory synchronization.

The index of a thread and its thread ID relate to each other in a straightforward way:
- For a one-dimensional block, they are the same
- For a two-dimensional block of size $(Dx,Dy)$, the thread ID of a thread of index $(x,y)$ is $(x+y\;Dx)$
- For a three-dimensional block of size $(Dx,Dy,Dz)$, the thread ID of a thread of index $(x,y,z)$ is $(x+y\;Dx+z\;Dx\;Dy)$

#### Grids of Thread Blocks

There is once again a hierarchical feature above 