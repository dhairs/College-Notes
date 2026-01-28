## Structure of the Repo

The `common` repo is structured with `/limine/` for bootloading, and `/src/` with the actual source of the kernel. Limine should remain untouched, it is copy pasted from the official codebases.

Additionally, there is a `/Makefile` in the project root. 

`limine.conf` in the repo root defines the way that Limine will boot the kernel.

`script.ld` is the LinkerScript file that defines the location each part of the program will be put into memory.

`src/system_main.cc` is the actual entry point to the kernel program.

## System Main

System main defines the requests to the bootloader through compile-time attributes.

```cpp
[[gnu::section(
    ".limine_requests")]] constexpr volatile BaseRevision base_revision{};
[[gnu::section(".limine_requests")]] constexpr volatile MultiProcessor mp{};
```

This file then reads all of these requests, wakes up every core using Limine's response (which includes a struct that can be updated to define a location to set the core to run at). Then, the core jumps to `core_main`.

For now, `core_main` simply checks what features are available on the processor and enables them. 

Then, each core runs `Thread::boostrap()` which simply "dresses up" the core to make the core seem like a thread to software.

It then points the thread to the thread control block in the FS register.

Finally, one real thread is created that runs kernel main. Kernel main is then added to the thread ready queue, and we run `impl:event_loop()` which then starts to do the logic for checking thread status and adding things to the ready queue / running it.