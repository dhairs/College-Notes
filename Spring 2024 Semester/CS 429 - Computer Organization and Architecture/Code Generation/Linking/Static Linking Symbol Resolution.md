
## Tasks of the Linker

- **Symbol resolution**: match every symbol reference with exactly one symbol definition
- **Relocation**: Merge `.text` and `.data` sections from multiple relocatable object modules in a coordinated manner to create one `.text` and one `.data` section. Do this with other sections similarly as well
- **Patching**: Modify symbol references to connect them "correctly" with the symbol definitions to which they have been resolved
- **Output creation**: generate the final binary executable

## Link-Time Symbols

A link-time symbol in a relocatable object module is a procedure, global variable, or `static` variable that is defined or referenced in the module.

Procedure parameters and procedure-local non-`static` program variables are of no interest to the linker, because they are handled through registers and activation records.

Procedure-local `static` variables are allocated in `.data` or `.bss` and are described in the module's symbol table.

## Symbols and Symbol Tables

The symbol table of an object module contains the information about the link-time symbols defined or referenced by the module.
- Attributes such as name, size, section, address, visibility, etc.

Define the following boolean predicates for a symbol $s$ in module $M$ (we'll refer to $s$ then as $M.s$)
- $\text{DEFINED}(s,M)$: true, if $s$ is defined *within* $M$, false otherwise
- $\text{REFERENCED}(s,M)$: true, if $s$ is referenced *within* $M$, false otherwise
- $\text{VISIBLE}(s,M)$: true, if $s$ is visible *outside of* $M$, false otherwise

A symbol in module $M$ is said to be:
- **Global** if $\text{DEFINED}(s,M)\wedge\text{VISIBLE}(s,M)$
- **Local** if $\text{DEFINED}(s,M)\wedge\neg\text{VISIBLE}(s,M)$ 
- **External** if $\neg\text{DEFINED}(s,M)\wedge\text{REFERENCED}(s,M)$

Among all the symbols **defined** in module $M$:
- Functions and initialized global data are called **strong definitions**
	- These are put into `.text`, `.data`, or `.rodata`
- Uninitialized or zero-initialized global data are called **weak definitions**
	- These are put into `.bss`

## Static Symbol Resolution

Local symbols are resolved at *compile-time*
- The compiler ensures that there's only one definition per module for each procedure-local symbol and creates unique names for procedure-local `static` variables
- The linker needs to do nothing with these

Global and external symbols are resolved at *static link-time*
- If the compiler encounters a global symbol in a module, it generates a link-time symbol definition in the module's symbol table for use by the linker
- If the compiler encounters an external symbol in a module, it generates a link-time symbol in the module's symbol table and passes it onto the linker to resolve
- The static linker tries to find a unique definition for this symbol reference among the symbol definitions available across all the modules that it is linking

This can be well-explained using graph theory:
 - Create a graph whose nodes are all the symbols of all the modules being linked. The node corresponding to symbol $s$ os module $M$ is called $M.s$
 - If the symbol reference $s$ of module $M$ is resolved to symbol definition symbol $t$ of module $N$, add the directed edge $(\text{REF}(M.s), \text{DEF}(N.t))$ 
 - The resulting graph is **bipartite**, with edges directed from references to definitions

### Rules of Symbol Resolution

We need a **singular** definition for each symbol

![Symbol Resolution Rules](Symbol%20Resolution%20Rules.svg)