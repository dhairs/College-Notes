
## What is a Process and Process Abstraction

A process is an abstraction that supports running programs

* Different processes may run several instances of the *same* program
* In most systems, processes form a tree, with the root being the first process to be created
* At a minimum, processes require the following resources:
	* Memory to contain the program code and data
	* A set of CPU registers to support execution of the program code
* The process *may* require the other extra resources, like:
	* I/O Access

The process abstraction controls the resource access for programs.

The first process in UNIX is `init`.

### The `init` process

As the name suggests, initializes things on the machine for other processes to work, and for the OS to function properly

## Programs

A program consists of:
- `code` — machine instructions
- `data` — variables stored and manipulated in memory, classified into
	- initialized variables (globals)
	- dynamically allocated variables (`malloc`, `new`, etc.)
	- stack variables (C automatic variables, function arguments)
- dynamically linked libraries (`DLL`'s)  — libraries that were not compiled or linked with the program (contained code & data, possibly shared with other programs that use them)
- mapped files — memory segments containing variables (`mmap()`), used frequently in database programs
	- similar to DLL's, these are also not part of the program itself
	- `mmap()` takes data from the disk and maps it into memory

This is explained in further detail in [[Object Modules and Linking]].