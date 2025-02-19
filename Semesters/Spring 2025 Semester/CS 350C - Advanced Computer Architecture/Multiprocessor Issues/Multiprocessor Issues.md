## Why

As we start to add cores to our processor, multiple events can be happening at once. As a result, subsystems that aren't necessarily on the processor itself (memory, external devices, etc.) need to be allocated and shrared correctly.

There are a bunch of different things that need to be handled correctly, some are:
- [[Memory Consistency and Cache Coherence]]