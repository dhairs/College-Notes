
## Tasks of the Linker

- **Symbol resolution**: match every symbol reference with exactly one symbol definition
- **Relocation**: Merge `.text` and `.data` sections from multiple relocatable object modules in a coordinated manner to create one `.text` and one `.data` section. Do this with other sections similarly as well
- **Patching**: Modify symbol references to connect then "correctly" with the symbol definitions to which they have been resolved
- **Output creation**: generate the final binary executable

## Link-Time Symbols

A link-time symbol in a relocatable object module is a procedure, global variable, or `static` variable that is defined or referenced in the module.

Procedure parameters and procedure-local non-`static` program variables are of no interest to the linker, because they are handled through registers and activation records.

Procedure-local `static` variables are allocated in `.data` or `.bss` and are described in the module's symbol table.

## Symbols and Symbol Tables

The symbol table of an object module contains the information about the link-time symbols defined or referenced by the module.
- Attributes such as name, size, section, address, visibility, etc.

Define the following boolean predicates for a symbol $s$ in module $M$ (we'll refer to $s$ then as $M.s$)
- $\text{DEFINED}()