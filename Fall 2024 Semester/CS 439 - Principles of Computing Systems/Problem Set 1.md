
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
	1. $2^5$ processes, so 31 processes are created because the original process should not be counted as a created process.
3. From Anderson and Dahlin, Ch1 question 1:  Suppose a computer system and all of its applications are completely bug free. Suppose further that everyone in the world is completely honest and trustworthy. In other words, we do not need to consider fault isolation.
    
    - How should the operating system allocate the processor? Should it give all of the processor to each application until it no longer needs it? If there are multiple tasks ready to execute at the same time, should it schedule the task with the least amount of work to do or the most? Justify your answer. **You should assume a uniprocessor.**
        - It would be best to schedule tasks using a first come first serve method because there is no worry of a user having an infinite loop or bug in their code that would hold up the queue. However, if there is already a list of tasks, it would make sense to queue them by the shortest task first so that each user gets the optimal response time.
        
    - How should the operating system allocate physical memory between applications? What should happen if the set of applications does not all fit in memory at the same time?
	    - The system should allocate physical memory by separating each application's memory space, so that each application believes it has access to all of the system memory. Then, the system can evict the least recently used application's memory when the new application requests more than is available.
4. From Anderson and Dahlin, Ch1 question 2:  Now suppose the computer system needs to support fault isolation (as in, if one process has a problem, then that problem should not affect other processes). What hardware and/or operating system support do you think would be needed to protect an application's data structures in memory from being corrupted by other applications? Assume more than one application may reside in memory at a time. 
	1. The operating system should be able to separate each process' memory. It would make sense to take in each pointer that the program requests, and map it to real, physical memory. Essentially make the program have virtual addresses that are translated by the machine. This way, if a program does manage to mess up some memory or edit another, it is only within its own memory space.
5. Run the following command in your command line (it generates 10k random integers less than 1000 and stores them in the num.txt file.):
   `$ for i in {1..10000}; do echo $(($RANDOM % 1000)); done > nums.txt`
   Now, without opening the file, answer the following questions with both a) the answer and b) the command you used to find the answer.
   1. How many numbers containing 74 are in the file?
	   1.  179 numbers containing 74
	   2. `grep "74" nums.txt | wc`
   2. How many 12s are in `nums.txt`?
	   1. 8 number 12's
	   2. `grep -w "12" nums.txt | wc`
   3. How many numbers in the file begin with 14?
	   1. 107 numbers begin with 14
	   2. `grep -E '14[0-9]' nums.txt | wc`
6. After testing with a simple function that returns a value + 1, and the `getuid` syscall, in our testing we found that system calls are on the order of 20 times slower than procedure calls. Running 100 procedure calls resulted in around a runtime of 1000ns, versus 100 system calls taking 20,000ns.
