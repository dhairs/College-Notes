
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

### Programs

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

#### Preparing Programs

![[Preparing a Program.svg]]

### Static vs. Dynamic Linking

Why use one over the other? There are many tradeoffs, including file size, memory usage, program runtime speed, portability, etc.

|                 | Static                                                    | Dynamic                                             |
| --------------- | --------------------------------------------------------- | --------------------------------------------------- |
| **Performance** | ✅ no lookup needed to find library (negligible)           | library needs to be looked up to execute in runtime |
| **Storage Use** | libraries are included in the program file                | ✅ library doesn't need to be included with file     |
| **Memory Use**  | larger program files must be loaded into main memory      | ✅ library added to process only when needed         |
| **Portability** | ✅ machine does not have to have library as it is included | machine must have the library to run the program    |
| **Patching**    | program has to be recompiled to include patch             | ✅ program does not need to be recompiled            |

### Running a Program

This is a multi-step process.

1. The OS creates a process with some memory allocated for it
2. The loader
	1. reads and interprets the header of the executable file
	2. sets up the process' memory to contain the code & data from the executable
	3. pushes `argc`, `argv`, `envp` onto the runtime stack
	4. sets the CPU registers properly and calls `__start()` (part of CRT0)
3. Program starts running at `__start`, which in turn calls `main()`
   We now say that the 'process' is running, no longer a 'program'
4. When `main()` returns, CRT0 calls `exit()` which destroys the process and returns all resources to the OS

## Anatomy of a Process

![[Anatomy of a Process.svg]]

### Process Context