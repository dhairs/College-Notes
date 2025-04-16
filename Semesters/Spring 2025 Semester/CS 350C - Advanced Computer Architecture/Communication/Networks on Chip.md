## Principles and Foundations of NoCs

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

> [!FAQ]+ How does latency grow when the load increases?
> Latency grows **exponentially** as the load increases. This means at near full loads we can get into a bunch of arbitration and latency issues.

## Fundamentals of NoCs

### Routers

Routers direct and buffer packets between input and output ports. They include routing logic, virtual channel allocators, and switch allocators. Typically, they use a 5-port design in a 2D mesh network (North, East, South, West, Local).

### Network Interfaces (NI)

Bridge between IP cores and the NoC as well as performing packetization/depacketization. Additionally, they do protocol conversion and address translation.

### Links

Links are physical connections between routers and are *typically* bidirectional. May contain multiple virtual channels.

## Communications Hierarchy

| Name                                              | Purpose                                                                                                                                                          |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Message**                                       | Sequence of bytes sent from a sending node to a receiving node.                                                                                                  |
| **Packet**                                        | Basic unit of data transfer containing routing information and payload. Every byte in a packet takes the same route.                                             |
| **Flit (FLow control unIT)**                      | Smaller units that make up packets. **Head flit**: contains routing information, **Body flits**: contains data payload, **Tail flit**: Marks end of packet.      |
| **Phit (PHysical transfer unIT, hardware-level)** | Transmitting a flit may take multiple cycles. Phit defines the number of cycles needed. E.g, if channel width is 32b, it takes 4 cycles to transmit a 128b flit. |
Thus, the communication hierarchy is as follows: $\text{Message}\to\text{Packet}\to\text{Flit}/\text{Phit}$.

### Interconnection Network Characteristics

**Topology**: the arrangement of nodes and channels into a graph where $G=(N,C),C\subseteq N\times N$.

**Routing**: the specification of how a packet chooses a path in this graph. The routing relation $R \subseteq C\times N\times C$ specifies a (possibly singleton) set of channels on which the packet can be routed given the channel occupied by the head of the packet and the destination node of the packet.

**Flow Control**: The protocol determining the allocation of channel and buffer resources to a packet as it traverses this path. E.g.: how resources are collected, how packet collisions over resources are resolved.

#### Topology of Interconnection Networks

A lot of different topologies: mesh, torus, folded torus, ring, fat tree.

Higher-radix topologies are generally harder to implement in NoCs.

In order for us to be able to route a packet from any node to any other node, we need a cyclic topology.

#### Routing Algorithms

We want to avoid routing cycles (to avoid deadlock) while also allowing a diverse number of paths. This will allow us to avoid network congestion.

**X-Y Routing (Dimension-Ordered Routing)**: first route along X dimension, and then Y. This is a simple implementation without deadlock. It can extend naturally to more dimensions, but it has no adaptivity to network conditions. It's mainly used in mesh NoCs. This is a simple and **deterministic** scheme. This method has a lack of diversity in the routes.

**Partially Adaptive**: west-first, North-last, Negative-first. Restrict turns to avoid deadlock. Limited adaptivity to congestion.

**Fully Adaptive**: Use virtual channels to avoid deadlock. Odd-even turn model. They have better load balancing and fault tolerance, however they require quite a bit more implementation complexity.

#### Flow Control

##### Credit Based

The basic problem is that we don't what what we should do if we don't have enough buffer space on the receiver's side. We can't just *drop* a flit. 

For this reason, we must also have some information at the sender about the free buffer space available at the receiver.

**Credit-based flow control**: the sender (A) maintains an estimate of the number of free buffers at the receiver (B). The sender sends a flit iff it thinks that the receiver has enough free buffers. Once the receiver frees a buffer, it sends a credit to the sender.

An improvement is on-off flow control:
- Off-threshold: stop sending messages
- On-threshold: resume sending messages.

##### Switching Techniques

**Circuit Switching**: establish complete path before transmission. 

**Packet Switching**:
- **Store-and-Forward**: full packet must arrive and be stored at a router before being forwarded.
- **Virtual Cut Through**: send flits before entire packet is buffered. Need to ensure that there is space for the entire packet.

**Wormholer S**