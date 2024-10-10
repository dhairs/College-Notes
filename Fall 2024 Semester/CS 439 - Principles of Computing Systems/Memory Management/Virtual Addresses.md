Use $n$-bits to represent *virtual* or *logical* addresses. A process perceives an address space extending from address $2^n-1$. The MMU translates from virtual addresses to real ones. The process no longer has to see real or physical addresses.

As a result, each process has the belief, the illusion, that it has access to all the memory on the system.