## What are Monitors

A programming language construct, very similar to what we call today objects.

Consists of:
- General purpose variables
- Methods
- Initialization code (constructor)
- Condition variables (can be either wait or signal)

### Example Declaration

```c
Monitor M {
	int a, b, c;
	condition x, y, z;
	fn1(...);
	fn2(...);
	...
	fnm(...);
}
```

### Hoare Monitors

Assume thread Q is waiting on condition $x$
Assume thread P is in the monitor
Assume thread P calls $x$.signal
P gives up monitor, P blocks
Q takes over monitor, Q runs
Q finishes up, gives up monitor
P takes over monitor, resumes

### Mesa Monitors (Per Brinch Hansen's Monitors)

Assume thread Q waiting on condition $x$
Assume thread P is in the monitor
Assume thread P calls $x$.signal
P continues, finishes
Q takes over monitor, runs
Q finishes, gives up monitor

