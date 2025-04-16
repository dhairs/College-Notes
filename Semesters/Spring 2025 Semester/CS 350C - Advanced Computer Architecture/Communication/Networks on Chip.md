## Principles and Foundations

Networks on Chip (NoC) are specialized interconnection networks facilitating communication between different components within a single chip using packet-based communication.

NoCs emerged in the early 2000s as a solution to the limitations of traditional bus based point-to-point interconnects.

### History

**Early 2000s**: First conceptual NoC papers by Dally & Towles and Benini & De Micheli

**Mid 2000s**: First prototypes and academic implementations

**2010s Onward**: Commercial adoption in many-core processors and SoCs

**2020s**: Integration with emerging technologies like photonics, wireless communication, and machine learning

## Evolution of On-Chip Communication

A **node** is any object that can send or receive a message (a Core, cache bank, memory controller, etc.).

Every communicating node has a **router** that orchestrates the communication on its behalf.

We *could* use a bus-based approach, it is simple, but often is very slow and not scalable.

Instead, we could create a Network on Chip (NoC). We can arrange a set of nodes as tiles. A router will then send and receive all messages for its tile, and forward messages originating at other routers to their destinations.

Routers are connected to adjacent routers with **links**.

> [!FAQ] How does latency grow when the load increases?
> Latency grows **exponentially** as the load increases.
