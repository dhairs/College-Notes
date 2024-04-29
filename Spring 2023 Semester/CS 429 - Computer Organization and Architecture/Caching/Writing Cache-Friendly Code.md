
## Why?
Because memory behavior dominates performance, we need to write programs in a way that makes good use of the memory hierarchy.

What methods?

The scope we'll focus on is Single function.

Focus:
- Inner loops with predictable access patterns (e.g., array access)
- Improving spatial locality

Assume the compiler handles temporal locality by placing scalar variables in registers

## Example 1: Vector Sum

