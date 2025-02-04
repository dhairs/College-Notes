## Optimizations

Code transformations must be done to improve the program, mainly to decrease execution time, but may also be used to decrease program size.

Optimizations **must** be safe. The resultant code must yield the same results as the original code, for **all possible executions**.

### Optimization Safety

Dead code elimination is a straightforward example. You can take code that isn't used at all, and remove it.

#### Example

```c
x = y + 1;
y = 2 * z;
if(d) x = y + z;
z = 1;
z = x;
```

Only the line `z = 1` is dead code in this ex