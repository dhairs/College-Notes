## Representing Programs

Remember the compilation process:
![[GCC Compilation Process.svg]]

The LD stands for the Linkage eDitor, and outputs executable

## Types of Object Files

An object file is a _self-describing_ block of bytes

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
  - We will discuss this one in depth

Fat binary: Multiple formats combined into one, which allows the binary to run on multiple systems

![[Object File Format.png]]

### ELF Format

The header is stored in 16 bytes, and it contains all the necessary information to bootstrap the file and run it.

All sections are variable-length.

#### ELF Format Structure

| ELF header (16 Bytes)      |     | bootstrapping information for the file                                                                                                                                                                                                                                                                                   |
| -------------------------- | --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `.text`                    |     | Machine code of compiled module. All the code goes into this section.                                                                                                                                                                                                                                                    |
| `.rodata`                  |     | Read-only global data (`printf` format strings, jump tables, etc.)                                                                                                                                                                                                                                                       |
| `.data`                    |     | Initialized global/static C variables                                                                                                                                                                                                                                                                                    |
| `.bss`                     |     | Uninitialized static C variables, including those initialized to 0 (saves space)                                                                                                                                                                                                                                         |
| `.symtab`                  |     | Symbol table — contains all the labels (functions) so that they can be "linked" between files                                                                                                                                                                                                                            |
| `.rel.text`                |     | List of `.text` locations that need to be 'relocated' (modified)                                                                                                                                                                                                                                                         |
| `.rel.data`                |     | List of `.data` locations that need to be 'relocated' (modified)                                                                                                                                                                                                                                                         |
| `.debug`                   | opt | Debugging symbol table — allows the debugger to map binary to source                                                                                                                                                                                                                                                     |
| `.line`                    | opt | Mapping between C line #'s and instructions in `.text`                                                                                                                                                                                                                                                                   |
| `.strtab`                  |     | String table for symbols in `.symtab`, `.debug`, and section names. <br><br>This serializes all of the strings (takes all of the strings in the file and puts them into a flattened array, with each string's null terminator encoded). This allows us to string turn pointers into indices to an array for the runtime. |
| Section Header Table (SHT) |     | Fixed-size entries describing each section. The ELF header describes where to find this header, and how many sections it contains                                                                                                                                                                                        |

#### Example

##### Source Files:

```c main.c
int sum(int *a, int n);

int array[2] = {1, 2};

int main(void) {
	int val = sum(array, 2);
	return val;
}
```

- The interface of `sum` is declared
- `sum` is _defined_ elsewhere
- `sum`is called (referenced)

```c sum.c
int sum(int *a, int n) {
	int i, s = 0;
	for (i = 0; i < n; i++)
		s += a[i];
	return s;
}
```

- The implementation of `sum` is defined
- The definition of `sum` happens to match the signature of the interface declared in `main.c`

##### Output of Object Files:

![[Main.c Object Linking Output.png]]

![[Sum.c Object Linking Output.png]]

##### Output of the Executable

![[Linking Example Output Executable.png]]

![[Linking Example Output 2.png]]

##### What would happen with different function signatures?

What if `sum` had a function signature of `int sum(int *a, int *b, int n)`?

There would be no issues with compilation, because type information is lost once we compile into a `.o` file. We simply have our assembly code, which contains nothing relating to types or function signature, we just have the name.

C++ solves this by "mangling" the name, and adding type information to the function name itself. This is especially important for function overloading.

#### Takeaways

The linker is not concerned with handing local variables and other symbols that are not visible outside individual object modules (static).

A module's **symbol table** provides information about the externally visible symbols defined in that module and the external symbols referenced by the module.

- These definitions and references must be matched, this process is called **symbol resolution**

The **relocation entries** of a module provide information about which symbol references in that module need to be adjusted (and how) when combining multiple object modules.

- Each object module is generated in isolation, in its local coordinate system
- We need to keep track of where to put each module, and put them into a single, global coordinate system for the final executable. We move code to new locations (hence "relocation")
- References must be connected to their resolved definitions, this is called **patching**

A variety of violations are detected by the linker, but not all conditions can be caught (e.g., different function signatures)

## Sources to Use:

https://courses.cs.washington.edu/courses/cse469/18wi/Lectures/02_Assembly.pdf

https://stackoverflow.com/questions/50957847/how-linkers-resolve-global-symbols-with-the-same-name-defined-at-multiple-places

https://www.sfu.ca/sasdoc/sashtml/iml/chap5/sect9.htm#:~:text=For%20each%20module%20you%20define,in%20its%20local%20symbol%20table.

https://observablehq.com/@benaubin/floating-point
