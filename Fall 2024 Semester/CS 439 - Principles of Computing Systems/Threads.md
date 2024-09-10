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
		CreateThread(write_data); // write threads will wait in I/O queue
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

Finally, look back at the web server from [[Threads#Example 3|Example 3]], we can rewrite this as:
```
create a number of threads, and for each thread, do:
	get network message from client
	get URL data from disk
	compose response
	send response
```

## The Cost of Threads

Just like anything in CS, threads are *not* free. They use less resources than making a new [[Process Abstraction|Process]], but you must still allocate a new stack for the thread, which adds overhead. Context switching still occurs.

## Threads vs. Processes

| Threads                                                                                   | Processes                                                                                |
| ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| No data segment or heap                                                                   | Code, data, heap, and other segments                                                     |
| Cannot live on its own, must live within process                                          | Must be at least one thread in process                                                   |
| Can be more than one thread in a process, first one calls `main` & has the process' stack | Threads within process share code/data/heap, I/O, but have individual stacks & registers |
| Inexpensive creation                                                                      | Expensive creation                                                                       |
| Inexpensive context switching                                                             | Expensive context switching                                                              |
| If a thread dies, its stack is reclaimed                                                  | If a process dies, its resources are reclaimed and all threads die                       |
In Linux, there is an idea of lightweight processes, somewhere between processes / threads, where each lightweight process shares the same code and data segments, but individual stacks.


## Thread Hazards

In a classical process (only one thread), the process' stack segment serves to be the stack of the root thread:
- The stack segment is far away from the code and data segments
- It grows implicitly during function calls up to the maximum size

In a multithreaded process, each thread needs a stack:
- Where should the stack be?
- What size?
- A thread has to be part of the process' address space

### Stack Allocation Options

**Allocate the stacks on the heap**

This is much easier than the alternative, but very hazardous because everything is in the same heap of the process' address space.

**Allocate the stack away from other stack segments**
This requires OS support, but is much safer because each stack is separate.

### Sharing

Consider the following code segment:
```c
int a = 1, b = 2;
main() {
	CreateThread(fn1, 4);
	CreateThread(fn2, 5);
}

fn1(int arg1) {
	if (a) b++;
}

fn2(int arg1) {
 a = arg1
}
```

Because threads use share the same heap, the value of `a` will be `5` and `b` will be `3` at the end of execution.

### Interleaving

Consider the following code segment
```c
int a = 1, b = 2;
main() {
	CreateThread(fn1, 4);
	CreateThread(fn2, 5);
}

fn1(int arg1) {
	if(a) b++;
}

fn2(int arg1) {
	a = 0;
}
```

We don't know which thread will run first, so we cannot say what the final result of the code execution will be. This is interleaving.

### Privacy & Sharing

Consider the following code segment:
```c
int a = 1, b = 2;

main() {
	CreateThread(fn, 4);
	CreateThread(fn, 5);
}

fn(int arg1) {
	int v = a + arg1;
	static l;
	if(v) {
		l = b++;
		v = 0;
	}
}
```

What are the values of `a`, `b`, `l`, and `v` at the end of execution?

`v` is created on each thread's stack, so it does not exist when the process is done with execution.

### Falling off the Cliff

Consider the following code segment:
```c
int a = 1, b = 2;
main() {
	CreateThread(fn, 4);
	CreateThread(fn, 5);
	CreateThread(fn, 6);
	// do some computation
	return 1;
}

fn() {
	a = b;
}
```

We didn't wait for our threads to finish their computation, we don't know if they finished or not.

When the main thread is returned, the process is reclaimed and no other computation is able to run in the threads.

### Protection

Consider the following code segment:

```c
int a = 1, b = 2, w = 1;
main() {
	CreateThread(fn);
	char *p = bogus value;
	*p = 4;
	while(w);
}

fn() {
	int v = a + b;
	w = 0;
}
```

What happens here?

Note that we have the bogus value for a pointer, when we try accessing that pointer, we'll get a segmentation fault, and that leads to an error state.

Our child thread has no exception, it should stay alive.

Killing the main thread is not possible because something has to call `exit` and return to CRT0. That's why if its the main thread causing the exception, we may as well just kill the whole process.

### Synchronization

```c
int a = 1, b = 2, w = 1;
main() {
	CreateThread(fn, 4);
	while(w);
}

fn() {
	int v = a + b;
	w = 0;
}
```

The main thread is able to wait for the child thread to complete before exiting.
### Concurrency

Consider the following code segment:
```c
int a = 1, b = 2, w = 1;
main() {
	CreateThread(fn, 4);
	CreateThread(fn, 5);
	while(w);
}

fn() {
	int v = a + b;
	w—;
}
```

This, in theory, should work. However, when the code actually executes, we have assembly under the hood that executes `w--;` in 4 instructions. Both threads are therefore loading the value of `w` into a register, and then doing the computation, and then storing.

As a result, there is a possible race condition where both processes load into the same registers (they share the same assembly), and the number calculated could therefore be `1`, instead of 0.

This code is non-deterministic. We don't know what will happen when it runs.

### Other Hazards and Concerns

If there is a signal, who should receive it?
- One thread?
- All thread?
- Some designated thread?

If there is an exception:
- Kill only the offending thread?
- Kill the process?

Hidden concurrency problems:
- Sharing through files\
- Shared variables

## Threads in Modern Programming Languages

### Java

```java
public class MyThread implements Runnable {
	public void foo() {
		System.out.println("Thread is running in the foo method!");
	}
	
	@Override
	public void run() {
		foo();
	}
	
	public statc void main(String[] args) {
		MyThread myThread = new MyThread();
		Thread thread = newThread(myThread);
		thread.start()
	}
}
```


### C++

```c++
class MyThread {
public:
	void foo() {
		std::cout << "Thread is running in foo method!" << std::endl;
	}
};

int main() {
	MyThread myThread;
	std::thread t(&MyThread::foo, & myThread);
	t.join();
	return 0;
}
```

### Python

```python
import threading
class MyTask:
	def foo(self):
		print("Task is running in foo method!")

task = MyTask()
t = threading.Thread(target=task.foo)
t.start()
t.join()
```

## Thread Variations

Threads differ according to three dimensions:
- Implementation: Kernel-level versus User-level
- Execution: Uniprocessor vs. multi-process
- Cooperative vs. uncooperative

This gives us 8 combinations.