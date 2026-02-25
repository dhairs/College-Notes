## Painting a Picture

Imagine we have a kernel, and have a `my_mod.c` file that defines some module that the kernel can use. This is not meant to be a standalone program, so it doesn't have a `main` entrypoint, but instead something like `mod_init()`.

We compile it to a `.o` file. We want this file to be able to integrate into the kernel without necessarily linking into it.

This requires some semblance of a dynamic linker/loader.