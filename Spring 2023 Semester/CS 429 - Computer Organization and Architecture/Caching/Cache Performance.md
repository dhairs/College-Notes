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
Our cache is defined as $\$_{1}=\$(A,B,C;S)$