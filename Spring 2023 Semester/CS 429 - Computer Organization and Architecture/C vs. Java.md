Note these 2 samples of code:

```java
class HelloWorld {

}
```

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

## Encapsulation
**C**:
- Uses Procedures and `structs`

**Java**:
- Uses objects, classes, and interfaces

## References
**C**:
- Makes pointers explicit (denoted by `*` or `&`)

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