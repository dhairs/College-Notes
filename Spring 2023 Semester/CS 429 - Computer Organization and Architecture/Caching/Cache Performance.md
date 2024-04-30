## Cache Management Overhead

$\$(A,B,C)$, where $\text{number of sets } S = \frac{C}{A\cdot B}$ 

Cache payload = $C$, $B=8C$ bits

Management overhead:
- Valid bits: $1\cdot S\cdot A\text{ bits}$
- Tag bits: $t\cdot S\cdot A\text{ bits}$, where $t=m-\log S-\log B$
- Dirty bits: $1\cdot S\cdot A\text{ bits}$
- Replacement bits: Approximately $\lceil \log A \rceil\cdot S\text{ bits}$

## Understanding Cache Misses

Each memory access can be defined as either a cache hit or cache miss

### Why do Cache Misses Happen
- Are cache misses happening because it is somehow **unavoidable**?
- Are cache misses happening because of the **limited capacity** of the cache?
- Are cache misses happening because of the **limited associativity** of the cache?

This leads to a cache miss classification model called the **3C model**

### The 3C Cache Miss Model
Our cache is defined as $\$_{1}=\$(A,B,C;S)$.

Based on our cache defined above, let's consider a fully-associative cache of the same block size and the same capacity: $\$_{3}=\$\left( \frac{C}{B}, B, C;1 \right)$

#### Compulsory Miss
Since we start with all the data in $M$ and nothing in $, the first access to **any memory block** is **necessarily** a miss. This is called a **compulsory miss**.
- This access would be a miss even in an infinite-capacity cache $\$_{2}=\$(A,B,\infty)$
- The number of compulsory misses is a tight *lower bound* on the minimum possible number of cache misses.

#### Capacity Miss
If a memory reference that is a non-compulsory miss in $\$_{1}$ is *also a miss* in $\$_{3}$, then limited associativity can't be the cause of the miss, and it must be because of limited capacity. This is called a **capacity miss**.

#### Conflict Miss
If a memory reference that is a non-compulsory miss in $\$_{1}$ is a *hit* in $\$_{3}$, then limited associativity is the cause of the miss. This is called a **conflict miss**.

## Memory Performance Equation
Let $R$ be the total number of memory references and let $M$ be the number of these references that miss in $. Define $m=\frac{M}{R}$ to be the miss rate and $h=1-m$ to be the hit rate. We *want* $h$ to be large and $m$ to be small.

Let $t_{h}$ be the hit time and let $t_m$ be the additionally miss penalty (both in processor cycles)
- Typically, $t_{h}\sim 1, t_{m}\sim 100$. 

**Average memory access time (AMAT)**: is $=h\cdot t_{h}+m\cdot(t_{h}+t_{m})=t_{h}+m\cdot t_{m}$
- e.g., if $m=0.1$, AMAT $=1+0.1\times 100=11$ cycles

### Memory Effects Dominate Performance
Compare the magnitudes of the numbers in the memory performance equation with the corresponding magnitudes in the [[Intro to Pipelining#Pipelining|Pipelining Performance Equation]].

The AMAT term would totally swamp out the *lp*, *mp*, and *rp* terms.

Furthermore, this is an average. An individual memory access takes between 1 to 101 cycles.

Dealing.
