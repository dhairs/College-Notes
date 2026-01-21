## Structure of a Kernel

A kernel will not be a single `.c` file (or at least it would be inefficient to do such). Instead, a codebase will usually consist of tons of different code and header files that are necessary for compiling and linking to a final executable.

Something like `gcc` is a compiler frontend, not the actual compiler engine itself. Calling `gcc` with some files is an intricate process that runs multiple different parts of the compilation process.

## Compilation Process

Recall how [[Object Modules and Linking|object modules and linking]] work.

![[GCC Compilation Process.svg]]

First, we go through the `cpp` (C pre-processor) which will ensure that the defines, imports, and preprocessor directives that are in files are injected with their actual values or whatever is necessary. This computation is happening at preprocess time, so it has no runtime impact.

Then, the preprocessed code is able to go through the [[Introduction to Compilers|compiler]] itself, which is `cc1` for C programs. At this point, the compiler performs a variety of [[Scalar Optimizations|scalar optimizations]], like [[Scalar Optimizations#Constant Folding|constant folding]].

That compiled code, which is now in assembly, is then passed to the assembler for the platform.

The assembler generates machine code which is then consumed by the linkage editor (linker) which then finally takes in all of the files to produce a runnable binary.