## Small Stacks

Split stacks allows the kernel to allocate a miniature stack, and enforce the compiler to check stack overflow wherever the stack is used to ensure that enough space is available. Additionally, the compiler must check that there is enough overflow to be able to call the function that can be used to allocate more memory.

The compiler, once overflowed, generates stubs to allocate a "stacklet" (small stack) and links it to the current stack. 

As the stack grows back down, it can follow its link to the previous stack to access certain variables.

Certain functions are allowed to support split stacks, and some can potentially not support it (think about the case where you may link with a library that was precompiled without any split stack flags or stubs).