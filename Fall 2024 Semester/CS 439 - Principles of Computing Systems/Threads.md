## The Case for Threads

### Example 1
**Consider the following program fragment:**
```C
main()
	read_data();      // read input data
	for(all_data)
		compute();    // do some computation
		write_data(); // output results to file
	endfor
```

**What is wasteful about a program like this?**
We don't compute while writing, so you waste time writing. Would be better if OS handles the writing in the background while we compute.


### Example 2
**Consider another fragment:**
```c
for(k = 0; k < n; k++)
	a[k] = b[k]*c[k] + d[k]*e[k]
```

Previous iterations don't affect the current iteration of the for loop, so theoretically we could fork or use parallel processing to do this. However, fork uses too many resources, double memory usage.

### Example 3
**Consider a web server**
```
get network message from client
get URL data from disk
compose response
send response
```

If you have many clients, you will be blocked for I/O and will develop a very large queue, can cause a crash, etc.

Would be nice to be able to overlap these.

## A Programmer's View of Threads

```c
main()
	some code
	tid = CreateThread(fn1, arg0, arg1, ...);
	// ... some more code

fn1(int arg0, int arg1, ...)
	some code
```

At the point CreateThread is called, execution continues in parent thread in the main function, and execution starts at `fn1` in the child thread. Both run in *parallel*.

So how can this help?

Remember the code segment from [[Threads#Example 1|Example 1]]. W can rewrite this as:

```c
main()
	read_data();      // read input data
	for(all_data)
		compute();    // do some computation
		CreateThread(write_data()); // write threads will wait in I/O queue
	endfor
```

Alternatively, look back at the code from [[Threads#Example 2|Example 2]]. We can rewrite as:

```c
CreateThread(fn, 0, n/2);
CreateThread(fn, n/2, n);

fn(I, m)
	for(k = I; k < m; k++)
		a[k] = b[k]*c[k] + d[k]*e[k];
```

In a two processor system, this is the fastest we can go because any more threads will force context switching.

Finally, look back at the web server from [[Threads#Example 3|Example 3]]
## The Cost of Threads

Just like anything in CS, threads are *not* free. They use less resources than making a new [[Process Abstraction|Process]], but you must still allocate a new stack for the thread, which adds overhead. Context switching still occurs.