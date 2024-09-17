## What are Semaphores

Semaphores are an implementation of blocking synchronization. 

A semaphore consists of:
- A variable $v$
- A thread list $L$
- A function $P$ (wait)
- A function $V$ (signal)

Syntax Example: `Semaphore s(5);`
