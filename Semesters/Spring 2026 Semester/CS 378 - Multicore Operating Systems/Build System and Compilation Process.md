## Structure of a Kernel

A kernel will not be a single `.c` file (or at least it would be inefficient to do such). Instead, a codebase will usually consist of tons of different code and header files that are necessary for compiling and linking to a final executable.

Something like `gcc` is a compiler frontend, not the actual compiler engine itself.

## Compilation Process

Recall how [[Object Modules and Linking|object modules and linking]] work.

![[GCC Compilation Process.svg]]

First, we go through the `cpp` (C pre-processor) which will ensure that the defines, imports, and preprocessor directives that are in files are injected with their actual values or whatever is necessary. This computation is happening at preprocess time, so it has no runtime impact.

