
## Hierarchical Directories

The file system is the [[Flat File Systems#Indexed Allocation|array of files]]. To humans, it is much easier to have something that is named.

![[File name and inode.svg]]

Each directory has `.` (current working directory) and `..` (parent directory)

By convention, the root directory is usually the first inode in the array
- the `..` directory to the root is itself

### Hard Links

This is possible because the name space is decoupled from the flat file system, files also have reference counts.

![[Hard Links.svg]]

We can't have hard links to directories because that would require a cyclic graph (we would need to have a reference to parent because then `..` could mean multiple things).

If we had a cycle, we could have floating islands that are no longer accessible which would need to be garbage collected, which would then be very slow on a large file system.

### Symbolic Links

Doesn't change reference count