## Background

What is sparsity? It is any tensor that is mainly comprised of 0s.

### Machine Learning Frameworks

Two types: 
- Define by run
	- Similar to interpreted languages
- Define and run
	- Similar to compiled languages

#### Compilers for Machine Learning

High level computational graph representations and do optimizations on them, similar to regular.

#### Compilers for Sparsity

**TACO**: Introduces storage methods for sparse tensors. Generalized sparse tensor expressions

## PyTorch Optimizations

`Torch.compile()` is a Just-in-Time (JIT) compilation method.

## Optimizing Graphs for Spacial Neural Networks

GNNS rely heavily on sparse matrix multiplications (SpMM)

SpMM dominates GNN execution time due to the sparsity of real-world graphs.

Performance depends significantly on the choice of sparse matrix format.

$$J(x,y)=\begin{pmatrix}\frac{\partial f}{\partial x} & \frac{\partial f}{\partial y} \\ \frac{\partial g}{\partial x} & \frac{\partial g}{\partial y}\end{pmatrix}=\begin{pmatrix}y-2 & x-1 \\ y & x\end{pmatrix}$$


