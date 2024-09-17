## What are Semaphores

Semaphores are an implementation of blocking synchronization. 

A semaphore consists of:
- A variable $v$
- A thread list $L$
- A function $P$ (wait)
- A function $V$ (signal)

**Important properties**:
- V(s) never blocks
- The insertion and removal from $L$ can be done at random
- In practice, a FIFO is mostly used, transforming the list into a queue
- The value $v$ gives how many processes are allowed in

Syntax Example: `Semaphore s(5);`

There are two types: 
- Counting semaphores
	- $v$ takes any value
- Binary semaphores
	- $v$ takes only 0 or 1

### Counting Semaphore Operations

```c
Initialization(val) {
	v = val;
	L = []
}
```
#### P(s)

```c
v—;
if(v < 0) {
	add thread to L;
	block;
}
```

This code executes atomically.

#### V(s)

```c
v++;
if (v <= 0) {
	remove a thread from L;
	Unblock(T);
}
```

This code executes atomically.

### Binary Semaphore Operations

#### P(s)

```c
if(v == 0) {
	Add caller to L;
	Block;
} else {
	v--;
}
```

This code executes atomically.
#### V(s)

```c
if(L != []) {
	Remove a thread from L;
	Unblock(T);
} else if(v == 0) {
	v = 1;
}
```

This code does not block.