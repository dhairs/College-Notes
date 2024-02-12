## What are Objects

In C, there are two types of objects:
- **Elemental**: declared *explicitly* - `int x`, `int* xp`, `float A[10]`, `node_t node`
	- Have identifiers as their names (`x`, `xp`, `A`, `node`)
	- May have either a basic or a derived type, type specification can surround name
- **Compound**: constructed *implicitly* - dereference `xp`, index to `A`, access a component of `node`
	- Has a tree structured name combining identifiers, constants, and *accessors* (`*xp`, `A[6]`, `node.children`, `node.children[0]`, `node.children[*xp]`)
	- May have either a basic or derived type: `int`, `float`, `(node_t*)[3]`, `node_t*` 
	- Type is inferred by a post order traversal of the tree

## Helper Methods

For a C object named `x`, define:
- `TYPE(x)` to be the C language type of `x`
- `ADDR(x)` to be the lowest numbered memory byte occupied by `x` at runtime (`&x`)
- `SIZ`