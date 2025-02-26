## Definition

The MESI protocol is a [[Sets|subset]] of the [[Cache Coherence#MOESI Model|MOESI protocol]].
## Snooping

The bus is in a serialized order and atomic itself, but the requests on it are not atomic.

Cache controller:

| ![[Snooping MESI.png]]                                                           |
| -------------------------------------------------------------------------------- |
| Figure 7.4 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |


Memory controller: 


| ![[Snooping Memory Controller MESI.png]]                                         |
| -------------------------------------------------------------------------------- |
| Figure 7.5 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

The problem with snooping is that the bus is atomic, and though it provides a totally ordered, serialized queue, it limits the speed of the cores and is hard to scale to a large amount of cores.

## Directory System Model


The directory system model looks like the following:

| ![[Directory System Model.png]]                                                  |
| -------------------------------------------------------------------------------- |
| Figure 8.1 https://pages.cs.wisc.edu/~markhill/papers/primer2020_2nd_edition.pdf |

The **directory** maintains a global view of the coherence state of each block. A cache controller wanting to send a `GetS` sends it directory to the directory, which then figures out what to do (which is either **respond** or **forward**). The interconnection network enforces point-to-point ordering of messages. The directory serves as the point of serialization of coherence transactions. Conflicting requests are processed by all nodes in per-block order, **not** in a total order.
- A requestor needs another strategy to determine when its request has been serialized.