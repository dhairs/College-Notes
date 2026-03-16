![[0331DF37-2B1F-463F-91DC-1CDBD67FC7FF2022-10-25_18-28-50_700.jpeg|300]]

Hi!

One of the first things we worked on was Exercise #6 which involved Vector1. This was a good way to see how a vector actually functions. I learned about the `initializer_list` class. This class is useful because it allows a vector to be created using a list of values inside curly braces. It makes the code look much simpler. We also looked at heap-allocated arrays. Managing memory on the heap is a big part of C++ and it is important to understand how it works to avoid errors.

We then studied `allocator` and `allocator_traits`. These tools are interesting because they separate the process of allocating memory from the process of constructing objects. In many cases, we use the `new` keyword which does both at the same time. However, using an allocator gives the programmer more control. I learned how to use `uninitialized_fill` and `uninitialized_copy` to put objects into raw memory. We also used the `destroy` function to call destructors without deallocating the memory itself. This level of detail was new to me but it is very useful for performance.

Paper #9 was about the Dependency Inversion Principle. This is a key part of solid software engineering. It suggests that high-level modules should not depend on low-level modules. Instead, both should depend on abstractions. This makes the code much easier to maintain and change in the future. We also started Project #3, which is a voting system. This project required a lot of logic to make sure the votes are counted correctly and that the program runs efficiently.

The collaborative quizzes were a highlight of the week. Talking with my classmates helps me see things from different perspectives. It also helps me identify which topics I need to spend more time studying. The programming challenges were fast, but they helped me practice solving problems when time is limited. I feel like I am making good progress in understanding how these complex systems work together.

My pick of the week is **Valgrind**. It is a programming tool that helps you find memory leaks and memory bugs in your C++ code. Since we are working with heap-allocated arrays and manual memory management, this tool is very helpful for making sure your program does not waste memory or crash.