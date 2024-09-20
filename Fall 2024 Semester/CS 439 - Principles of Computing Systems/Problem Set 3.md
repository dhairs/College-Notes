1. Given the following piece of code:
    
    main(int argc, char**argv)
    {
       int child=fork();
       int c=2;
       
       if(child==0)
       {
          c+=2;
       }
       else
       {
          child=fork();
          c+=4;
          if(child==0)
             c+=2;
       }
    }
    
    How many different copies of the variable c are there? What are their values?
	    **There are 3 copies of `c`. The values are 4, 6, and 8**
    
2. Consider a uniprocessor kernel that user programs can trap into using system calls. The kernel receives and handles interrupts from I/O devices. Would there be any need for critical sections within that kernel?
	1. **Yes, there is the possibility of important data being accessed when an interrupt is handled, that can cause the data to be lost.**
    
3. Describe the priority inversion problem and give an example situation where it may occur.
	1. **Priority inversion is when a high priority task is delayed running because a lower priority task holds a lock to an exclusive resource that the high priority task relies on. As a result, a lower priority task that doesn't rely on that same thing can run, effectively allowing lower priorities to run before the highest. This could happen in a situation on, for example, a mars rover.**
    
4. Compare and contrast monitors and semaphores. What is an appropriate use of each?
	1. **Monitors allow mutual exclusion for a resource. Once a thread or process is accessing a resource with a monitor, it can be the only one. However, in semaphores, multiple threads and processes can access the same resource, effectively making it a shared resource. Also, monitors are basically objects, encapsulating the methods, data structures, etc. of a shared item. A semaphore is controlled by the OS.**
    
5. Deadlock can exist if and only if several conditions hold simultaneously. What are those conditions _within a process_? Name and describe all of them.
	1. **Deadlock can occur when multiple threads hold an exclusive lock to a resource that another thread needs to use to be able to run a routine, while also not holding enough locks to run the routine needed. Essentially, each process can only hold a number of locks that is less than necessary to carry out its tasks.**
    
6. Consider the following program fragment:
    
       if(a > 0)
          sema_down(s1);
       else
          sema_down(s2);
       
       b++;
       
       sema_down(s3);
       
       if(b < 0 && a <= 0)
          sema_down(s1);
       else if(b >= 0 && a > 0)
          sema_down(s2);
       else
          sema_down(s4);
       
       a++;
       
       sema_up(s4);
       sema_up(s3);
       sema_up(s2);
       sema_up(s1);
       
       
    
    s1, s2, s3 and s4 are semaphores initialized to 1. All variables are automatic (on the stack). Now, consider two threads running this fragment of code simultaneously, can there be a deadlock? Why, or why not?
		**Yes, there can be deadlock because each semaphore is initialized to 1, it is binary. As a result, when the first thread runs, it acquires s1, but another thread can acquire s2 (because of the if-else statement), this leads to then the code blocking.**
    
7. Some number of neighbors are sharing a bike to train for various sporting events. Since each neighbor will train daily and also must rest for his or her big event, they are hoping for an easy way to share the bike that allows only one rider to be on the bike at a time and allows the riders to rest while waiting for the bike. You are a known expert at synchronization problems involving limited resources, and so they have turned to you to devise a solution.
    
    Write the following function:
    

```c
Semaphore s(1);

void borrow_bike() {
	extern Semaphore s;
	P(s);
	// ride bike/train/do whatever
	V(s);
};

V(s) {
	L.remove(threadPID);
	unblock;
}

P(s) {
	L.add(threadPID);
	block;
}
```
     
    
    which may be executed by multiple neighbors (threads) at a time, using:
    
    1. semaphores, and
    2. monitors.
    
	Keep in mind that when each neighbor will need the bike is unpredictable, and neighbors should be able to rest from the time they request the bike until they acquire it.