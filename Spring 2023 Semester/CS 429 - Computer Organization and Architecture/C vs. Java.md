# C vs. Java

Note these 2 samples of code:

**`Java`**:

```java
class HelloWorld {
	public static void main(String[] args) {
	System.out.println("Hello, world!");
		for (int i = 0; i < args.length; i++) {
			System.out.printf("%d: %s\n", i, args[i]);
		}
	}
}
```

**`C`**:

```c
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[]) {

	fprintf(stdout, "Hello, world!\n");
		for(int i = 0; i < argc; i++) {
			printf("%d: %s\n", i, argv[i]);
		}
	
	return EXIT_SUCCESS;
}
```

Both do the same thing effectively, but note the differences. Java's `io` is built into the language and doesn't require imports. Everything is also made its own class. C is procedural, and lacks the ability to make objects. 

The `*argv[]` in C represents an array of pointers to characters, which are effectively strings that are terminated by the `NUL` character.

## Encapsulation
**C**:
- Uses Procedures and `structs`

**Java**:
- Uses objects, classes, and interfaces

## References
**C**:
- Makes [[pointers]] explicit (denoted by `*` or `&`)

**Java**:
- Abstract object references automatically managed by the compiler/language

## Strings
**C**:
- Uses a null-terminated array of `char`s (where null is denoted as `\0`)

**Java**:
- Uses a built in `java.lang.String` class
- Strings represent objects

## Parameters
**C**:
- Always is pass by value
- For this reason, pointers have to be explicitly entered

**Java**: 
- Passes the value of the reference of an object
- Essentially only passes the value if it is primitive, reference if it is an object

## Memory Management/Allocation
**C**:
- Memory must be manually allocated, using `malloc`

**Java**:
- Allocates memory for objects when created using `new`
- Memory is cleared using the JVM Garbage Collector

## "Objects"
**C** refers to variables as "objects," and they are used interchangeably. Note that it is purely just a reference in memory in C.