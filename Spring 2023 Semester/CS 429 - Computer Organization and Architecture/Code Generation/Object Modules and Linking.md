## Representing Programs

Remember the compilation process:
![[GCC Compilation Process]]

The LD stands for the Linkage eDitor, and outputs executable

## Types of Object Files

An object file is a *self-describing* block of bytes

This is similar to storing the tree in the header of a Huffman encoded file, or the metadata for a [[Dynamic Memory Management|malloc]] memory block.

There are three types:
- **Relocatable**: Binary code and data, suitable for combining (e.g. `p1.o` and `p2.o`)
- **Shared**: A special type of relocatable object file that can be loaded into memory and linked dynamically, either at load time or at run time (the file `libc.so`)
	- Note: this is what as `.dll` is on Windows
- **Executable**: Binary code and data, suitable for being copied into memory and executed (e.g. the file `p`)

### Object File Formats

Different formats on different systems:
- UNIX (originally): `a.out`
- Windows: Portable Executable (PE)
- MacOS-X: Mach Object (Mach-O)
- AArch64/Linux: Executable and Linkable Format (ELF)
	- We will discuss this one

Fat binary: Multiple formats combined into one, which allows the binary to run on multiple systems