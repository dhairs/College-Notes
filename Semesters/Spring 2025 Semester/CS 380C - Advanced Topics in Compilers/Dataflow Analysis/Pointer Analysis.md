## Heap Allocation

The **simplest solution** is to use one node in a points-to graph to represent all the heap cells. This simply tells you that something is a pointer to the heap, not where in the heap.

The more **elaborate solution**, however, is to use a different node for each malloc site in the program. This way, you can track each location in the heap.

The **even more elaborate solution** is to use something called **shape analysis**. The goal is to summarize potentially infinite data structures but keep around enough information so we can disambiguate pointers from stack into the heap if possible.

## Summary

| Less Precise        | More Precise      |
| ------------------- | ----------------- |
| Equality-based      | Subset-based      |
| Flow-insensitive    | Flow-sensitive    |
| Context-insensitive | Context-sensitive |
There is no consensus about which technique to use. If you are using context-insensitive, may as well also be flow-insensitive.