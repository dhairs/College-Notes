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
	- We will discuss this one in depth

Fat binary: Multiple formats combined into one, which allows the binary to run on multiple systems

### ELF Format

The header is stored in 16 bytes, and it contains all the necessary information to bootstrap the file and run it.

All sections are variable-length.

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
- `sum` is *defined* elsewhere
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