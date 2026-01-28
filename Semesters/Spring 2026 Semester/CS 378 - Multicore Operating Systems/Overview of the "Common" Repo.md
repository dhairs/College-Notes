## Structure of the Repo

The `common` repo is structured with `/limine/` for bootloading, and `/src/` with the actual source of the kernel. Limine should remain untouched, it is copy pasted from the official codebases.

Additionally, there is a `/Makefile` in the project root. 

`limine.conf` in the repo root defines the way that Limine will boot the kernel.

`script.ld` is the LinkerScript file that defines the location each part of the program will be put into memory.