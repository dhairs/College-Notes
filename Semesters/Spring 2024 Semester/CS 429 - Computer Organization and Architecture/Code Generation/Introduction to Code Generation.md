# Code Generation

First, we need to understand how and where variables are stored in memory, because that is a large part of how we generate code for them.

## Where are Variables Stored?

Local variables are stored in the function's stack frame
- The typical addressing mode is `[SP, #pimm]`

Global variables are stored at locations named by labels
- The typical addressing mode is `label`
- Need to use `ADRP` and `ADR` instructions to reach the address

## Code Generation for Basic Types

| C Source Code        | Type   | A64 Assembly Code                                                                                            |
| -------------------- | ------ | ------------------------------------------------------------------------------------------------------------ |
| `int x, y, z *w`     | `NA`   | `x is in memory at [sp, #24], y @ [sp, #20], z @ [sp, #16], w @ [sp #8]`                                     |
| `x = 2`              | `int`  | `mov w9, #2` &#10; `str w9, [sp, #24]`                                                                          |
| `y=x`                | `int`  | `ldr w9, [sp, #24` &#10; `str w9, [sp, #20]`                                                                    |
| `x++`                | `int`  | `ldr w9, [sp, #24]`&#10;`add w9, w9, #1`&#10;`str w9, [sp, #24]`                                               |
| `y -= x`             | `int`  | `ldr w10, [sp, #24]`&#10;`ldr w9, [sp, #20]`&#10;`subs w9, w9, w10`&#10;`str w9, [sp, #20]`                     |
| `z = x + y - 4`      | `int`  | `ldr w10, [sp, #24]`&#10;`ldr w9, [sp, #20]`&#10;`add w9, w9, w10`&#10;`subs w9, w9, #4`&#10;`str w9, [sp, #16]` |
| `w = &x`             | `int*` | `add x8, sp, #24`&#10;`str x8, [sp, #8]`                                                                      |
| `z = *w`             | `int`  | `ldr x10, [sp, #8] // load W`&#10;`ldr w9, [x10]     // load X`&#10;`str w9, [sp, #16] // store in Z`          |
| `unsigned i, int *E` |        | `i @ [sp #60]`&#10;`E @ [sp, #48]`                                                                            |
| `int x = E[i]`       |        | `ldr x8, [sp, #48]`&#10;`ldr w9, [sp, #60]`&#10;`ldr w8, [x8, x9, `                                            |
