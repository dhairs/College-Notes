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

The `.a` file extension signifies a collection of `.o` object files.

> [!NOTE] Shared Object Files/Dynamically Linked Libraries
> *Note*: there is also the possibility of shared object files (`.so` Linux, `.dll` Windows, `.dylib` macOS). These can be referenced by other programs without necessarily needing to copy the actual object file to the program. It helps with decreasing program size. 
> 
> In the above picture, you can see the inclusion of `libc.so` as a reference in the linking stage.

Additionally, you also need to have a `LinkerScript` (`.ld`) file that defines the way the compiler will place object sections in memory. This is **very** important for embedded systems and kernels that are running directly on hardware. It defines where things exist in memory, where data will be, how things should be loaded into memory, etc. 

> [!faq] Why have I never needed to write a LinkerScript?
> The compiler provides a default when there is no linker script explicitly defined. This allows for defining a stable linked executable for a machine, without giving the user control over placement in memory. 

In a kernel, you need to have direct control over where things will be placed by the compiler to ensure hardware works correctly. We can usually ensure things happen with `__attribute__(<attribute>)` (compiler extension directives) in order to tell the compiler to do something. In C++, we can do `[[<attribute>]]`.