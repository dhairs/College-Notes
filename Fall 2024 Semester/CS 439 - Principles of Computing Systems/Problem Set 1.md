
1. What are the three methods of switching from user mode to supervisor mode? When might each occur?
	1. Trap Instruction
		1. This might occur when a user program uses a system call or "trap instruction," like requesting for more memory with malloc
	2. Exception
		1. This might occur when a user program attempts to access memory no longer allocated to it — this would cause a SEGFAULT (an exception) and cause the OS to come in to handle the exception.
	3. Interrupts
		1. This might occur when an I/O Device sends a message to the system, for example, a user presses a physical button on their keyboard, which invokes the OS to direct the interrupt to the correct interrupt handler — or handle the interrupt itself.
2. Given the following piece of code:
   ```C
	main(int argc, char** argv)
	   {
	      forkThem(5);
	   }
	
	   void forkThem(int n)
	   {
	      if(n>0)
	      {
	         fork();
	         forkThem(n-1);
	      }
	   }
	```
	How many processes are created if the above piece of code is run?
	1. $2^5$ processes, so 32 processes are created.
3. From Anderson and Dahlin, Ch1 question 1:  
    Suppose a computer system and all of its applications are completely bug free. Suppose further that everyone in the world is completely honest and trustworthy. In other words, we do not need to consider fault isolation.
    
    - How should the operating system allocate the processor? Should it give all of the processor to each application until it no longer needs it? If there are multiple tasks ready to execute at the same time, should it schedule the task with the least amount of work to do or the most? Justify your answer. **You should assume a uniprocessor.**
        - 
        
    - How should the operating system allocate physical memory between applications? What should happen if the set of applications does not all fit in memory at the same time?
    - 