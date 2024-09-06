
1. What are the three methods of switching from user mode to supervisor mode? When might each occur?
	1. Trap Instruction
		1. This might occur when a user program uses a system call or "trap instruction," like requesting for more memory with malloc
	2. Exception
		1. This might occur when a user program attempts to access memory no longer allocated to it — this would cause a SEGFAULT (an exception) and cause the OS to come in to handle the exception.
	3. Interrupts
		1. This might occur when a user presses a physical button on their keyboard, which invokes the OS to direct the interrupt to the correct interrupt handler — or handle the interrupt itself.
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
	1. 5
3.  