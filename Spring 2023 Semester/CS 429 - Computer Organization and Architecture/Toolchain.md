## Using GDB (GNU Debugger)

`cond n [expression]`

This is basically to set breakpoints if you want to only stop when a certain condition is met.

"`break foo if i == 4`"

`next (n)` - steps one line of code, stepping **over** functions

`step (s)` - steps one line of code, stepping **into** functions

`print <expression>` prints any C expression.

## Using LLDB (Low-Level Debugger)

If you're on an ARM Mac, (any M-series), you'll need to use LLDB to debug C and C++ code.

